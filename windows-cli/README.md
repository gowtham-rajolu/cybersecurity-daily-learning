# Windows CLI: Beginner Field Notes

These notes are a starting point for getting comfortable with Windows from the command line. The aim is not to memorise commands. It is to understand what a command tells you, recognise the output and know what to check next.

**Focus:** CMD, PowerShell, files and folders, system details, local users and groups, and basic networking.

**Lab rule:** Practise on your own Windows computer or a Windows VM that you control. Read a command before running it. Do not change accounts, firewall rules or system settings just to make an exercise work.

---

## 1. CMD and PowerShell are different shells

A terminal is the window where you type. CMD and PowerShell are command interpreters (shells) that run inside a terminal.

| | Command Prompt (CMD) | PowerShell |
|---|---|---|
| Program | cmd.exe | powershell.exe (Windows PowerShell 5.1) or pwsh.exe (PowerShell 7+) |
| Main use | Traditional Windows commands and batch files | Administration, automation and scripting |
| Pipeline | Mainly passes text | Passes .NET objects between commands |
| Script files | .bat and .cmd | .ps1 |
| Typical command style | dir, cd, type | Get-ChildItem, Set-Location, Get-Content |

Windows PowerShell 5.1 is included with supported Windows installations. PowerShell 7 is a separate, newer installation. Windows Terminal is a terminal application that can host CMD, Windows PowerShell and PowerShell 7; it is not itself a shell.

### Why PowerShell commands look different

PowerShell cmdlets commonly use a Verb-Noun naming style:

- Get-Location — get the current folder.
- Get-ChildItem — list items in a folder.
- Set-Location — move to another folder.
- Get-Content — read a file.

PowerShell also has aliases such as ls, dir, cat and pwd. In PowerShell these are aliases for PowerShell commands; they are not proof that CMD understands the same syntax. When learning, use the full cmdlet name so you know which shell you are using.

### Find help instead of guessing

Run these in PowerShell:

~~~powershell
Get-Command Get-ChildItem
Get-Help Get-ChildItem
Get-Help Get-ChildItem -Examples
Get-Alias ls
$PSVersionTable
~~~

- Get-Command finds commands available in the current session.
- Get-Help explains how a command works. Some help content may need to be downloaded with Update-Help; you can still use -Examples where available.
- Get-Alias shows what an alias points to.
- $PSVersionTable identifies the PowerShell version.

In CMD, use:

~~~cmd
help
commandname /?
~~~

Replace commandname with a command you want help for, for example ipconfig /?.

---

## 2. Understand Windows paths

A Windows path often begins with a drive letter:

~~~text
C:\Users\YourUserName\Documents
~~~

Useful path ideas:

- C:\ is the root of the C: drive.
- .\ means the current folder.
- ..\ means the parent folder.
- A path with spaces should be wrapped in quotation marks.
- PowerShell's $HOME variable points to your user profile folder.

Examples:

~~~powershell
Set-Location $HOME
Set-Location "C:\Program Files"
Get-Location
~~~

Do not assume that the current folder is the same every time a terminal opens. Check it with Get-Location (PowerShell) or cd (CMD).

---

## 3. Day 1: navigation and file commands

Start PowerShell. You do not need Administrator rights for these exercises.

### See where you are and what is there

~~~powershell
Get-Location
Get-ChildItem
Get-ChildItem -Force
Get-ChildItem -File
Get-ChildItem -Directory
~~~

- Get-Location prints the current working directory.
- Get-ChildItem lists files and folders in that location.
- -Force also displays hidden items.
- -File and -Directory filter the results.

### Create a practice folder and a text file

~~~powershell
New-Item -ItemType Directory -Name CyberLab
Set-Location .\CyberLab
New-Item -ItemType File -Name day1.txt
Set-Content -Path .\day1.txt -Value "My first Windows CLI note."
Get-Content .\day1.txt
~~~

What happened:

1. New-Item created a folder.
2. Set-Location moved into it.
3. New-Item created an empty file.
4. Set-Content wrote text to the file (and replaces its existing contents).
5. Get-Content displayed the file contents.

### Add, copy, rename and move

~~~powershell
Add-Content -Path .\day1.txt -Value "Practising PowerShell."
Copy-Item .\day1.txt .\day1-copy.txt
Rename-Item .\day1-copy.txt -NewName .\backup.txt
New-Item -ItemType Directory -Name Archive
Move-Item .\backup.txt .\Archive\
Get-ChildItem -Recurse
Test-Path .\Archive\backup.txt
~~~

- Add-Content appends text instead of replacing the file.
- Copy-Item makes a copy.
- Rename-Item changes a name.
- Move-Item moves an item.
- Test-Path checks whether a path exists and returns True or False.
- Get-ChildItem -Recurse lists items in the current folder and its subfolders.

**Be careful with deletion.** Remove-Item can permanently remove files or folders. Do not practise deletion against important folders. If you later need to test a command that supports it, use its -WhatIf option first to preview the action.

### CMD equivalents

Open CMD separately to try these equivalents in a test folder:

| Task | CMD |
|---|---|
| Show current folder | cd |
| List items | dir |
| Change folder | cd CyberLab |
| Go to parent | cd .. |
| Create folder | mkdir CyberLab |
| Create a simple file | echo Hello > day1.txt |
| Display a text file | type day1.txt |
| Copy a file | copy day1.txt copy.txt |
| Rename a file | ren copy.txt backup.txt |
| Move a file | move backup.txt Archive\ |

The PowerShell and CMD commands are not interchangeable in every situation. Check which shell is open before copying a command.

---

## 4. System information

Start with a few commands that answer different questions:

~~~powershell
hostname
whoami
$PSVersionTable
systeminfo
~~~

| Command | What it tells you |
|---|---|
| hostname | Computer's network name |
| whoami | Account currently running the shell |
| $PSVersionTable | PowerShell version and edition |
| systeminfo | Windows edition, build, hardware and other system details |

A more focused PowerShell view:

~~~powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsBuildNumber, OsArchitecture, CsName
Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, BuildNumber, OSArchitecture, LastBootUpTime
~~~

The output can be long. Select-Object keeps the fields you want to inspect.

### Hostname versus username

These identify different things:

- hostname identifies the computer.
- whoami identifies the account currently running the command.

A computer can have several user accounts, but it has one configured computer name at a time.

---

## 5. Users, groups and privileges

For security work, first establish **which account is running a command** and **what permissions that account has**. Do not assume that being logged in means you are an administrator.

### Check your current identity

~~~powershell
whoami
whoami /user
whoami /groups
whoami /priv
~~~

- /user shows the account's security identifier (SID).
- /groups lists groups in the current security token.
- /priv lists privileges in the current security token. A listed privilege is not necessarily enabled or usable in every situation.

### List local accounts and groups

~~~powershell
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember -Group "Administrators"
~~~

These commands inspect local Windows accounts and groups. On some editions or configurations, the LocalAccounts module may not be available in every PowerShell session. If a command is not recognised, record the exact error rather than trying random fixes.

CMD alternatives:

~~~cmd
net user
net localgroup
net localgroup Administrators
~~~

### Understand the terms

- User account: an identity used to sign in or run a process.
- Group: a collection of accounts that can share permissions.
- Standard user: normally has limited rights to change system-wide settings.
- Administrator: can perform more system-wide actions, subject to Windows security controls.
- UAC (User Account Control): prompts or uses elevation controls when an action needs administrative rights. A UAC prompt is not proof that the program requesting elevation is safe.

For now, only inspect accounts and groups. Do not add users, change passwords or add accounts to Administrators as part of this beginner exercise.

---

## 6. Basic networking from PowerShell

These commands help you understand the network configuration of your own Windows machine.

### IP address and adapter configuration

~~~powershell
ipconfig /all
Get-NetIPConfiguration
Get-NetIPAddress -AddressFamily IPv4
~~~

Look for the active adapter, IPv4 address, subnet mask or prefix, default gateway and DNS servers. An address beginning with 169.254 often indicates that Windows did not receive an IPv4 address from DHCP.

### Local neighbour information

~~~powershell
arp -a
Get-NetNeighbor -AddressFamily IPv4
~~~

These show neighbour/ARP information known to the machine. They do not provide a complete inventory of every device on a network.

### Connections and listening ports

~~~powershell
netstat -ano
Get-NetTCPConnection
~~~

In netstat output:

- Local Address and Foreign Address show the two endpoints.
- State shows the TCP connection state, such as LISTENING or ESTABLISHED.
- PID is the process ID associated with the connection.

To identify a process from a PID, substitute the actual number shown in your output:

~~~powershell
Get-Process -Id 1234
~~~

The example PID 1234 is only a placeholder; use a PID from your own output.

A more compact PowerShell view:

~~~powershell
Get-NetTCPConnection | Select-Object -First 20 LocalAddress, LocalPort, RemoteAddress, RemotePort, State, OwningProcess
~~~

### DNS and a basic connectivity test

~~~powershell
nslookup example.com
Resolve-DnsName example.com
Test-NetConnection example.com -Port 443
~~~

- nslookup and Resolve-DnsName query DNS.
- Test-NetConnection checks connectivity to the specified host and port. TcpTestSucceeded indicates whether the TCP connection test succeeded.

You can also inspect the routing table:

~~~powershell
route print
Get-NetRoute -AddressFamily IPv4
~~~

Only test systems and networks you own or have permission to assess. These commands are for understanding your own configuration, not for scanning unrelated networks.

---

## 7. Common beginner problems

| Problem | What to check |
|---|---|
| Command is not recognised | Confirm whether you are in CMD or PowerShell; check spelling and use Get-Command in PowerShell. |
| Access is denied | The current account may not have permission. Do not automatically run everything as Administrator. |
| File is not found | Run Get-Location, then Get-ChildItem; check the path and spelling. |
| Path contains spaces | Put the full path in quotation marks. |
| Output is too long | Use Select-Object to show only useful fields. |
| PowerShell and CMD syntax differ | Identify the shell first and use its own command syntax. |

Useful habits:

~~~powershell
Get-Location
Get-Command <command-name>
Get-Help <command-name> -Examples
Get-History
~~~

Replace <command-name> with the command you want to investigate. Press Ctrl+C to stop a command that is still running.

---

## 8. Day 1 practice exercise

Use your own Windows account. Try to complete these without copying an answer from someone else.

- [ ] Open PowerShell and identify the current directory.
- [ ] Display the files and folders in that directory.
- [ ] Create a folder named PentestLab in your user profile.
- [ ] Inside it, create a file named day1.txt.
- [ ] Write one sentence to the file and display its contents.
- [ ] Copy the file, rename the copy and move it into a subfolder.
- [ ] Find your computer name and current username.
- [ ] Display your IPv4 configuration and DNS servers.
- [ ] Display your current TCP connections and identify one PID.
- [ ] Explain, in your own words, the difference between hostname and whoami.

When writing up the exercise, record the command, a short description of what it did, and one useful detail from the output. Do not publish private IP details, usernames, machine identifiers or other personal system information in a public repository.

---

## 9. A 30-day route after Day 1

| Days | Focus |
|---|---|
| 1–5 | CMD and PowerShell basics, paths, files and folders |
| 6–10 | Windows system information, hardware and installed updates |
| 11–15 | Users, groups, security identifiers and permissions |
| 16–20 | IP configuration, DNS, routes, ports and connections |
| 21–25 | Processes, services and scheduled tasks |
| 26–30 | Event logs, Defender status and basic PowerShell scripting |

Move on when you can explain the commands and interpret the important parts of their output. Speed comes with repetition.

---

## 10. Quick reference

| Goal | PowerShell | CMD |
|---|---|---|
| Current folder | Get-Location | cd |
| List files | Get-ChildItem | dir |
| Change folder | Set-Location | cd |
| Read file | Get-Content | type |
| Computer name | hostname | hostname |
| Current user | whoami | whoami |
| System details | Get-ComputerInfo / systeminfo | systeminfo |
| IP configuration | Get-NetIPConfiguration / ipconfig | ipconfig |
| Connections | Get-NetTCPConnection / netstat -ano | netstat -ano |
| DNS lookup | Resolve-DnsName / nslookup | nslookup |

## Microsoft documentation

- [PowerShell documentation](https://learn.microsoft.com/powershell/)
- [PowerShell command discovery](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/get-command)
- [Get-ChildItem reference](https://learn.microsoft.com/powershell/module/microsoft.powershell.management/get-childitem)
- [Windows command-line reference](https://learn.microsoft.com/windows-server/administration/windows-commands/windows-commands)
- [Windows User Account Control](https://learn.microsoft.com/windows/security/application-security/application-control/user-account-control/)

**Study note:** This is a learning guide, not a record that every exercise has been completed. Add your own command output and observations after practising, but remove private system details before publishing them.
