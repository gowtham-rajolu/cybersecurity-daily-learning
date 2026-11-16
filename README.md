# Cybersecurity Learning Journal

This is where I'm keeping my cybersecurity study notes. I'm working through networking, Linux, Nmap, web security, penetration testing labs and the defensive/SOC side as well.

I don't want this to become a folder of copied definitions. The useful parts for me are the commands I tried, what the output means, what went wrong and what I need to revisit.

**Started:** 1 June 2026 (requested journal start date)  
**GitHub:** [gowtham-rajolu](https://github.com/gowtham-rajolu)

## What I'm learning

| Topic | Current focus | Notes |
|---|---|---|
| Fundamentals | CIA triad, threats, vulnerabilities and risk | [Fundamentals](fundamentals/README.md) |
| Networking | IP addresses, subnetting, ports, DNS and routing | [Networking](networking/README.md) |
| Linux | Permissions, processes, services and logs | [Linux](linux/README.md) |
| Windows CLI | CMD, PowerShell, files, system details, users and networking | [Windows CLI](windows-cli/README.md) |
| Recon | Host discovery and Nmap service enumeration | [Reconnaissance](reconnaissance/README.md) |
| Web security | HTTP, uploads, sessions and common web flaws | [Web security](web-security/README.md) |
| Metasploit | Understanding modules and using a safe target VM | [Metasploit](metasploit/README.md) |
| Privilege escalation | Linux and Windows enumeration | [Privilege escalation](privilege-escalation/README.md) |
| SOC / SIEM | Logs, alerts and basic investigation | [SOC notes](soc-siem/README.md) |
| Practice | TryHackMe and Hack The Box | [TryHackMe](tryhackme/README.md) · [HTB](hackthebox/README.md) |

## Journal entries

- [12 Nov 2026](daily-notes/2026-11-12.md) — Web lab, file uploads, Python venv and grep
- [13 Nov 2026](daily-notes/2026-11-13.md) — Nmap, Metasploit, Metasploitable and VPN troubleshooting
- [15 Nov 2026](daily-notes/2026-11-15.md) — Setting up this journal and deciding how to track progress
- [16 Nov 2026](daily-notes/2026-11-16.md) — TryHackMe UnrealIRCd backdoor lab, reverse shell troubleshooting and access verification

The journal was requested to start from 1 June, but I don't have reliable notes for every day since then. I have not filled those gaps with made-up study sessions. The older dated notes are summaries of topics visible in my learning conversations; their file dates are not proof of commits on those dates.

## How I want to use this repo

After a study session I'll try to write down:
- what I was trying to understand;
- the command or lab step I used;
- what I expected and what actually happened;
- the mistake or confusing part;
- what I understand now, and what is still unclear.

I'll use the [daily note template](templates/DAILY-NOTE.md), but I don't need to fill every heading if it doesn't fit that day's work.

## Lab safety

I will keep practice to my own machines, local vulnerable VMs and platforms where I have permission. Vulnerable VMs should stay isolated. I won't commit passwords, tokens, private keys, hashes or sensitive target information. I also won't publish TryHackMe flags or answers where the platform's rules prohibit it.

## Folder layout

```text
fundamentals/       basic security concepts
networking/         TCP/IP, ports, DNS and routing
linux/              Linux commands and administration
windows-cli/        CMD and PowerShell fundamentals
reconnaissance/     Nmap and enumeration
web-security/       HTTP and web application security
metasploit/         framework notes and lab work
privilege-escalation/
soc-siem/
tryhackme/
hackthebox/
daily-notes/        dated study notes
monthly-reports/
templates/
resources/
```

## Things I still need to work through

- [ ] Get more comfortable with subnetting and routing
- [ ] Understand TCP connection setup properly
- [ ] Practice Nmap options and read scan output carefully
- [ ] Learn HTTP requests in Burp Suite
- [ ] Set up and enumerate a Metasploitable VM safely
- [ ] Learn Linux privilege-escalation checks
- [ ] Get comfortable with Windows CLI and PowerShell enumeration
- [ ] Start working with sample SOC logs
- [ ] Write up complete labs with evidence and remediation

This is a learning record, not a claim that I already know everything listed above.
