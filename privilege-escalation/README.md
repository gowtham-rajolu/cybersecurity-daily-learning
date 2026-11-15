# Privilege escalation notes

Privilege escalation means getting more permissions than the account or process was meant to have. I need to learn how to spot the configuration mistakes that can make this possible, and how to fix them.

## Linux checks to understand

In an authorised lab, start by looking at the current user and the machine:

```bash
id
uname -a
cat /etc/os-release
sudo -l
ps aux
systemctl --type=service --state=running
find / -type f -perm -4000 2>/dev/null
```

Finding an unusual SUID file or a permissive sudo rule is not automatically a vulnerability. I need to understand the owner, permissions, binary, configuration and whether the behaviour can actually be abused.

## Windows topics on my list

- Local users and groups
- Service permissions
- Scheduled tasks
- Unquoted service paths
- Token privileges
- Patch level and security settings

## What a useful lab note should say

Record the initial user/permission level, the configuration issue, the evidence, what impact it could have and how an administrator should fix it. Don't include secrets or use these techniques on machines without permission.
