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

## Recent lab observation — 16 November 2026

During an authorised TryHackMe UnrealIRCd exercise, my first command shell identified its user as `webmaster`. Later in the same lab, I successfully authenticated over SSH as `root` and verified access to the root home directory.

I also encountered a credential-like entry in a system file. I have intentionally left its contents out of this public repository. I am not documenting the exact credential or claiming a complete privilege-escalation path yet: I still need to understand why the file was readable, how the credential was obtained and what authentication configuration allowed the root SSH login.

This is an observation to investigate further, not a reusable credential or a complete vulnerability explanation. The [daily lab note](../daily-notes/2026-11-16.md) records the context without publishing secrets or flags.

## Windows topics on my list

- Local users and groups
- Service permissions
- Scheduled tasks
- Unquoted service paths
- Token privileges
- Patch level and security settings

## What a useful lab note should say

Record the initial user/permission level, the configuration issue, the evidence, what impact it could have and how an administrator should fix it. Don't include secrets or use these techniques on machines without permission.
