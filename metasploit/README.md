# Metasploit Framework and Metasploitable Labs

## What they are

- **Metasploit Framework** is a penetration-testing framework with modules for auxiliary checks, exploits, payloads, encoders, and post-exploitation workflows.
- **Metasploitable** is an intentionally vulnerable training system. It is a target environment, not a scanning tool.

Nmap, Wireshark, Burp Suite, and Metasploit have different roles: discovery, packet analysis, web proxy/testing, and exploitation framework respectively.

## Lab safety

Run vulnerable targets in an isolated host-only or private lab network. Do not bridge them to an untrusted network or expose them to the internet. Snapshot the VM before exercises.

## Basic framework orientation

```bash
msfconsole
help
search type:auxiliary name:scanner
info <module>
show options
```

Only configure and run modules against explicitly authorized lab targets. Read module documentation and understand side effects before execution.

## Learning workflow

1. Identify a lab service using Nmap.
2. Research the service and version.
3. Determine whether a relevant vulnerability is present.
4. Read the Metasploit module documentation.
5. Validate safely in the isolated lab.
6. Capture evidence and explain remediation.
7. Restore the lab snapshot.

## Key distinction

A vulnerability scanner or exploit module result is not automatically proof of compromise. Validate with controlled evidence and document uncertainty.
