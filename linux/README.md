# Linux notes for security labs

I use Ubuntu for a lot of my practice, so I want to be comfortable moving around the filesystem and checking what's running before I start using security tools.

## Directories I should recognise

- `/etc` — system configuration
- `/var/log` — many system and service logs
- `/home` — user home directories
- `/tmp` — temporary files
- `/proc` — process and kernel information

## First commands to run

```bash
whoami
id
pwd
ls -la
stat filename
```

These tell me which user I'm running as, which groups I belong to, where I am and what permissions a file has.

## Permissions

Linux permissions are shown for owner, group and others. The basic bits are read (`r`), write (`w`) and execute (`x`).

```bash
chmod 640 filename
chown user:group filename
find /var/log -type f
```

I need to understand the effect of a permission change before running it, especially with recursive options.

## Processes, services and sockets

```bash
ps aux
top
systemctl status ssh
journalctl -u ssh --since today
ss -tulpn
```

These help me check running processes, service state, service logs and listening ports. Some commands need elevated privileges to show all details.

## Logs

On Ubuntu/Debian, authentication logs are often in `/var/log/auth.log`. Some RHEL-based systems use `/var/log/secure`. The exact location depends on the distribution and logging setup.

## Things to practise

- [ ] Find a file and inspect its permissions.
- [ ] Explain what `640` means in chmod.
- [ ] Check which process owns a listening port.
- [ ] Read SSH service logs.
- [ ] Understand what `sudo -l` reports.
- [ ] List running systemd services.

Use sudo only when needed. Don't run a command from a tutorial as root until I understand what it changes.
