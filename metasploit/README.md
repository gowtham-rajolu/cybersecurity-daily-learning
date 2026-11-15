# Metasploit and Metasploitable notes

I asked about installing Metasploit on Ubuntu and how the framework is used. I also needed to clear up what Metasploitable actually is.

## Framework vs target

- **Metasploit Framework** is the testing framework. It has auxiliary, exploit, payload and post modules.
- **Metasploitable** is an intentionally vulnerable machine made for practice. It is the target VM, not a tool like Nmap.

The rough workflow makes more sense to me now: find a service, identify what is running, research it, then decide whether there is a safe way to validate a weakness in the lab.

## Getting familiar with the console

```bash
msfconsole
```

Inside the console:

```text
help
search type:auxiliary
info <module>
show options
```

I should read the module information and required options before running anything. A module result is not automatically proof that a system was compromised.

## What I learned in the UnrealIRCd lab

In an authorised TryHackMe room, I searched for UnrealIRCd and selected the backdoor module:

```text
search UnrealIRCd
use exploit/unix/irc/unreal_ircd_3281_backdoor
show options
```

The target's IRC service was on TCP port 6667. I used the VPN interface address for the reverse connection callback. My first listener port was 443, and the handler failed with `Errno::EACCES` while trying to bind. This was a local permission issue because ports below 1024 are privileged on Linux. I changed the listener to an unprivileged port and the handler started.

The module then reported that a command shell session had opened. In that session, `whoami` returned `webmaster`.

One mistake I made: I typed `whoami` at the Metasploit module prompt before a session existed. Metasploit executed it on my own machine, which returned my local username. That output was not evidence about the target. I need to confirm a session is open and interact with it before interpreting shell output as remote.

The full session notes, including the basic Nmap results and what I still need to understand, are in [16 November's journal entry](../daily-notes/2026-11-16.md).

## Module, payload and handler

- **Exploit module:** the code that attempts to trigger the vulnerability.
- **Payload:** the action or code path used after the vulnerability is triggered.
- **Handler:** waits for and manages the incoming connection for a reverse payload.

These are related but not interchangeable. Selecting a payload does not select an exploit, and configuring options does not prove exploitation succeeded.

## Lab setup notes

Keep the vulnerable VM on a host-only or otherwise isolated network. Don't expose it to the public internet. Taking a VM snapshot before testing makes it easier to restore the lab afterwards.

## Practice plan

1. Start the isolated Metasploitable VM.
2. Confirm its lab IP from the VM/network settings.
3. Use Nmap to identify exposed services.
4. Research one service and understand why it might be vulnerable.
5. Read the relevant Metasploit module documentation.
6. Test only if the exercise is in scope.
7. Save evidence and write down how the issue could be fixed.
8. Restore the snapshot.
