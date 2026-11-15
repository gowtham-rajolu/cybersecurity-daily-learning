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

I haven't recorded a successful exploit in this file. These are setup and learning notes, not a completed machine write-up.
