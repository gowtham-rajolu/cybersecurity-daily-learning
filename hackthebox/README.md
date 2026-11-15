# Hack The Box notes

I'll use this folder for HTB Academy modules and machine notes. I haven't written up a completed machine here yet, so this is just the checklist I want to follow.

## Before starting

- Read the machine/module description and scope.
- Connect to the VPN if the exercise requires it.
- Check that the VPN interface and route are present.

Useful checks:

```bash
ip -br addr
ip route
ip route get <lab-ip>
ping -c 3 <lab-ip>
```

Ping might be blocked, so a failed ping doesn't settle whether the target is reachable.

## While working

1. Record the target address privately and keep to the assigned target.
2. Do basic host and service discovery.
3. Save scan output so I can refer back to it.
4. Research each exposed service before trying an exploit.
5. Keep notes on what worked, what failed and why.

## Write-up reminders

For each machine, I want to include the starting point, enumeration commands, important output, the reasoning behind each step, the access path, remediation and anything I still don't understand.

Don't publish flags or platform answers if the rules say not to. Never scan outside the assigned scope.
