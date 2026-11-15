# Cybersecurity Daily Learning Journal

A practical, evidence-conscious journal for learning cybersecurity: networking, Linux, reconnaissance, web security, penetration testing, SOC operations, and lab write-ups.

> **Journal period:** 1 June 2026 onward  
> **Owner:** [@gowtham-rajolu](https://github.com/gowtham-rajolu)  
> **Status:** Active learning journal

## Purpose

This repository records concepts studied, commands practiced, lab observations, mistakes, and next steps. Historical entries are reconstructed only where prior learning conversations provide evidence. A dated note is not proof that a Git commit was made on that date; GitHub contribution dates reflect actual commits.

## Learning roadmap

| Area | Focus | Notes |
|---|---|---|
| Foundations | CIA triad, risk, threat, vulnerability | [Fundamentals](fundamentals/README.md) |
| Networking | TCP/IP, ports, DNS, routing, subnetting | [Networking](networking/README.md) |
| Linux | Shell, permissions, processes, services | [Linux](linux/README.md) |
| Reconnaissance | Nmap discovery, port and service enumeration | [Recon](reconnaissance/README.md) |
| Web security | HTTP, sessions, authentication, OWASP risks | [Web security](web-security/README.md) |
| Exploitation labs | Metasploit, Metasploitable, validation | [Metasploit](metasploit/README.md) |
| Privilege escalation | Linux and Windows enumeration concepts | [Privilege escalation](privilege-escalation/README.md) |
| Defensive security | Logs, SIEM, alert triage, incident response | [SOC & SIEM](soc-siem/README.md) |
| Practice platforms | Guided labs and write-ups | [TryHackMe](tryhackme/README.md) · [HTB](hackthebox/README.md) |

## Dated journal

- [2026-11-12 — Web penetration testing, lab workflow and security projects](daily-notes/2026-11-12.md)
- [2026-11-13 — Nmap, Metasploit, Metasploitable and network troubleshooting](daily-notes/2026-11-13.md)
- [2026-11-14 — No verified dated entry yet](daily-notes/README.md)
- [2026-11-15 — Learning journal setup and study roadmap](daily-notes/2026-11-15.md)

These entries are based on the available learning history, not fabricated historical Git commits. Add a note when you actually study; commit it that day to build a genuine contribution streak.

## Daily workflow

1. Pick one focused topic.
2. Read documentation and understand the underlying concept.
3. Practice in an authorized lab or on systems you own.
4. Record commands, expected output, actual observations, and mistakes.
5. Add a short summary and tomorrow's next step.
6. Commit your work.

Use [the daily template](templates/DAILY-NOTE.md) for each study session.

## Safety and ethics

- Test only systems you own or have explicit written permission to assess.
- Keep vulnerable machines isolated in a lab network.
- Never upload credentials, tokens, private keys, personal data, or target-sensitive information.
- Redact IP addresses and hostnames when a lab requires confidentiality.
- Treat scan results as observations, not proof of exploitability.

## Repository map

```text
.
├── fundamentals/
├── networking/
├── linux/
├── reconnaissance/
├── web-security/
├── metasploit/
├── privilege-escalation/
├── soc-siem/
├── tryhackme/
├── hackthebox/
├── daily-notes/
├── monthly-reports/
├── templates/
└── resources/
```

## Progress

- [ ] Networking fundamentals
- [ ] Linux fundamentals
- [ ] Nmap enumeration
- [ ] HTTP and web security
- [ ] OWASP Top 10
- [ ] Metasploit fundamentals
- [ ] Linux privilege escalation
- [ ] SOC and SIEM fundamentals
- [ ] Complete documented lab write-ups

**Consistency over volume. Learn, test safely, document honestly.**
