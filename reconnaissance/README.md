# Reconnaissance and Nmap notes

Recon is where I start building a picture of an authorised lab target: which hosts are reachable, which ports respond and what services might be running.

## Commands I'm learning

```bash
# Basic scan of an authorised lab host
nmap <lab-ip>

# Scan only selected ports
nmap -p 22,80,443 <lab-ip>

# Probe for service/version information
nmap -sV <lab-ip>

# Run Nmap's default NSE scripts as well
nmap -sC -sV <lab-ip>

# Read targets from a file
nmap -iL targets.txt

# Save results in normal, XML and grepable formats
nmap -oA results/lab-scan <lab-ip>
```

Only put targets in `targets.txt` if they're included in my lab scope. I should inspect what a script does before using it on a real engagement.

## Options I need to remember

| Option | Meaning |
|---|---|
| `-sn` | Host discovery without a port scan |
| `-p` | Choose ports |
| `-sV` | Probe services for version information |
| `-sC` | Run the default NSE script set |
| `-O` | Attempt OS detection |
| `-oA` | Save output in several formats |
| `-iL` | Read targets from a file |

## Reading the result

- `open`: something is accepting connections on that port.
- `closed`: the host responded, but no application is listening there.
- `filtered`: filtering or lack of response stopped Nmap deciding whether it is open or closed.

A version string doesn't prove a vulnerability. I need to check the service and its configuration before writing a finding.

## My scan workflow

1. Confirm the target and allowed scope.
2. Check whether the host is reachable.
3. Scan the ports I need.
4. Identify the services.
5. Look into the services one at a time.
6. Save the output and note anything uncertain.

## References

- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [Nmap NSE documentation](https://nmap.org/book/nse.html)
