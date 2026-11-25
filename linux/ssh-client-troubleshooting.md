# SSH client troubleshooting notes

**Date:** 25 November 2026  
**Topic:** Understanding SSH connection diagnostics

SSH (Secure Shell) provides an encrypted connection to a remote system. It is commonly used for remote administration and secure file transfer.

## 1. Basic connection

```bash
ssh username@server
ssh -p 2222 username@server
```

- The first command connects to the server's default SSH port (usually TCP 22).
- `-p` selects a different server port.
- Replace the example username, host and port with values supplied for an authorised system.

## 2. Verbose debugging

```bash
ssh -v username@server
ssh -vv username@server
ssh -vvv username@server
```

The flags increase diagnostic detail:

- `-v`: verbose client messages.
- `-vv`: more detailed debugging.
- `-vvv`: maximum SSH client debugging output.

Useful things to look for include which configuration files are read, which identity files are considered, key-exchange progress, host-key checks and authentication methods offered by the server.

Verbose output is diagnostic evidence, not proof that a connection succeeded. Read the final error and the surrounding lines to identify the stage that failed.

## 3. Common files

| Path | Purpose |
| --- | --- |
| `~/.ssh/config` | Per-user SSH client configuration |
| `~/.ssh/known_hosts` | Host keys remembered by the client |
| `~/.ssh/id_ed25519` | Example private key (keep secret) |
| `~/.ssh/id_ed25519.pub` | Matching public key |

Never publish a private key. A public key is designed to be shared with the remote account or service that should accept it.

## 4. Select an identity explicitly

```bash
ssh -i ~/.ssh/id_ed25519 username@server
```

The `-i` option tells the client which identity file to try. The private key must be readable only by its owner; if SSH rejects overly broad permissions, inspect and correct the file permissions rather than making the key more accessible.

## 5. A simple troubleshooting sequence

1. Confirm the hostname or IP address and port.
2. Check network reachability and whether the SSH service is listening (where you have permission).
3. Run the client with `-v` and identify the stage where it stops.
4. Check the username and the authentication methods accepted by the server.
5. Confirm that the intended key is being offered.
6. Verify host-key changes through a trusted channel before accepting them.

A changed host-key warning can indicate a legitimate server rebuild, but it can also signal an interception risk. Do not blindly delete the old entry or disable host-key checking.

## 6. Useful server-side checks

On an Ubuntu system where you have administrative access:

```bash
systemctl status ssh
sudo journalctl -u ssh --since today
sudo ss -tlnp
```

The service may be named `sshd` on other distributions. Logs and process details may require elevated privileges.

## 7. Practice checklist

- [ ] Compare the amount of output from `ssh -v`, `-vv` and `-vvv`.
- [ ] Identify the identity file SSH attempts to use.
- [ ] Explain the difference between a private key and a public key.
- [ ] Locate the client's `known_hosts` file.
- [ ] Explain why an unexpected host-key change must be verified.

## Safety reminder

Only test SSH against systems you own or are explicitly authorised to access. Review verbose logs before sharing them because they can reveal usernames, hostnames, IP addresses and local file paths.
