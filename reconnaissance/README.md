# Reconnaissance and Nmap

Reconnaissance gathers information about an authorized target to understand its exposed attack surface. Keep scans within the scope and rate limits of the lab or engagement.

## Nmap basics

```bash
# Scan a lab host
nmap 192.0.2.10

# Scan selected TCP ports
nmap -p 22,80,443 192.0.2.10

# Detect service versions
nmap -sV 192.0.2.10

# Run default safe discovery scripts plus version detection
nmap -sC -sV 192.0.2.10

# Scan targets listed in a file you are authorized to assess
nmap -iL targets.txt

# Save normal, XML, and grepable output
nmap -oA results/lab-scan 192.0.2.10
```

## Common options

| Option | Purpose |
|---|---|
| `-sn` | Host discovery without port scan |
| `-p` | Select ports |
| `-sV` | Probe open ports for service/version |
| `-sC` | Run default NSE scripts |
| `-O` | OS detection (may require privileges) |
| `-oA` | Save output in multiple formats |
| `-iL` | Read targets from a file |

## Interpret results carefully

- `open`: an application is accepting connections on the port.
- `closed`: reachable, but no application is listening.
- `filtered`: Nmap cannot determine the state due to filtering or lack of response.

Version detection is an estimate. Confirm findings with service-specific evidence.

## Suggested workflow

1. Confirm scope and authorization.
2. Discover live hosts.
3. Scan only in-scope ports.
4. Identify services and versions.
5. Enumerate services using appropriate safe methods.
6. Record evidence, timestamps, and limitations.
7. Validate findings without causing disruption.

## References

- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [Nmap NSE documentation](https://nmap.org/book/nse.html)
