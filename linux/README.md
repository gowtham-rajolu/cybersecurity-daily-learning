# Linux for Security Practitioners

## Filesystem and permissions

- `/`: filesystem root
- `/etc`: system configuration
- `/var/log`: common log location
- `/home`: user home directories
- `/tmp`: temporary files
- `/proc`: process and kernel information

Linux permissions are represented for owner, group, and others: read (r), write (w), execute (x).

```bash
whoami
id
pwd
ls -la
stat filename
chmod 640 filename
chown user:group filename
find /var/log -type f
```

## Processes and services

```bash
ps aux
top
systemctl status ssh
journalctl -u ssh --since today
ss -tulpn
```

## Log review

Review authentication and service logs using the distribution's logging setup. Common locations include `/var/log/auth.log` (Debian/Ubuntu) and `/var/log/secure` (some RHEL-based systems). Access may require elevated privileges.

## Safe privilege model

Use sudo only for tasks that require it. Understand the command before running it. Avoid piping unknown remote scripts directly into a privileged shell.

## Learning checklist

- [ ] Navigate and search files
- [ ] Explain rwx and octal permissions
- [ ] Inspect processes and listening sockets
- [ ] Read authentication logs
- [ ] Explain sudo and least privilege
- [ ] Identify systemd services
