# Privilege Escalation — Study Notes

Privilege escalation occurs when an account or process gains permissions beyond those intended.

## Linux enumeration concepts

In an authorized lab, understand how to inspect:
- Current identity and groups
- Operating system and kernel version
- Running processes and services
- File and directory permissions
- Sudo policy
- Scheduled tasks
- Installed packages and exposed services

Useful read-only commands:

```bash
id
uname -a
cat /etc/os-release
sudo -l
ps aux
systemctl --type=service --state=running
find / -type f -perm -4000 2>/dev/null
```

Do not assume that every SUID binary or unusual permission is exploitable. Investigate ownership, expected behavior, configuration, and version.

## Windows topics to learn

- Local users and groups
- Service permissions
- Scheduled tasks
- Unquoted service paths
- Token privileges
- Patch level and security configuration

## Reporting

For each finding, document the initial access level, the misconfiguration, evidence, impact, remediation, and cleanup. Never use these techniques on systems without permission.
