# TryHackMe notes

This folder is for notes from rooms I actually work through. I have previously been working on a guided web pentesting exercise and asked about the upload page, Python virtual environments, VPN connectivity and grep. The recap is in [my 12 November notes](../daily-notes/2026-11-12.md).

## UnrealIRCd lab — 16 November 2026

I worked through an UnrealIRCd 3.2.8.1 backdoor exercise over the TryHackMe OpenVPN connection. The dated write-up is in [my 16 November journal entry](../daily-notes/2026-11-16.md).

What I verified during the session:
- The `tun0` interface was the VPN interface and supplied the callback address for the lab tunnel.
- A basic Nmap scan found SSH (22/tcp) and IRC (6667/tcp).
- SearchSploit returned several UnrealIRCd references, including a Metasploit module and a separate Perl downloader/execute script.
- The first reverse handler attempt failed because local port 443 could not be bound by my unprivileged process. Changing to an unprivileged port allowed the handler to start.
- The Metasploit session opened as `webmaster`. A later SSH login as `root` was also successful; I am keeping the credential, target address and flag values out of this public repository.

I also learned to distinguish commands run by the local Metasploit console from commands typed into an established remote shell. See the daily note for the mistakes and follow-up topics.

## Next practice session — 20 November 2026

I prepared a checklist for the Basic Pentesting room. This is a plan for the next hands-on session, not a completed-room report: [20 November learning log](../daily-notes/2026-11-20.md).

## Enumeration & Brute Force — 24 November 2026

I practised web application enumeration and testing a numerical password-reset token flow using Python `requests`. The room-specific notes cover session cookies, response inspection, token formatting and defensive lessons: [Enumeration & Brute Force](enumeration-and-brute-force.md).

## Speed Chatting — 28 November 2026

Completed the LoveConnect / Speed Chatting web application lab. I documented Nmap service detection, Werkzeug identification, frontend route discovery, the profile-picture upload form, upload testing, the Python reverse-shell callback, root access verification and defensive takeaways: [Speed Chatting lab notes](speed-chatting.md).

## What I want to record for each room

- Room name and the date I worked on it
- What the room is teaching
- Which machine or service is in scope
- Commands I tried and what they returned
- Where I got stuck
- How I worked through the problem
- What the result tells me
- How the issue could be prevented or detected

I don't need to write a long report for every room. The important thing is to explain the steps in my own words and keep enough detail that I can repeat the learning later.

Keep credentials and sensitive target information out of the repo. Don't publish flags, answers or room content where TryHackMe rules prohibit it.
