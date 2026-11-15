# Hack The Box Learning Notes

Use this directory to record HTB machine and Academy learning.

## Suggested methodology

1. Read the machine or module scope.
2. Confirm VPN connectivity and routes.
3. Perform scoped host discovery.
4. Enumerate exposed services.
5. Research likely weaknesses.
6. Validate findings in the provided environment.
7. Document access path and defensive remediation.
8. Clean up local artifacts and stop lab instances.

## Troubleshooting VPN connectivity

```bash
ip -br addr
ip route
ip route get <lab-ip>
ping -c 3 <lab-ip>
```

Ping may be blocked. Check routes and test only the expected lab service if the platform permits. Never scan outside the assigned target scope.
