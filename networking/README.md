# Networking notes

Networking is one area I need to get solid at for both pentesting and SOC work. These are the terms and commands I want to keep close while practising.

## Addressing and routing

- An IP address identifies an interface on an IP network.
- A subnet prefix/mask tells me which part is the network.
- The default gateway is where traffic goes when there isn't a more specific route.
- DNS looks up names such as A/AAAA records.
- DHCP gives a device its network configuration.
- A MAC address is used at the local link layer.

## TCP vs UDP

TCP sets up a connection and provides ordered, reliable delivery. UDP doesn't set up a connection in the same way and doesn't guarantee delivery or ordering. I shouldn't assume UDP is always faster or TCP is always safer; it depends on the application.

## Ports worth recognising

| Port | Common service |
|---:|---|
| 21 | FTP |
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 123 | NTP |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |

A port number is only a starting clue. I still need to identify the actual service.

## Commands to practise on my own machine

```bash
ip -br addr
ip route
ip route get 1.1.1.1
ip neigh
resolvectl status
ss -tulpn
ping -c 4 1.1.1.1
traceroute example.com
dig example.com
```

## When a lab target won't connect

This is the order I want to check instead of randomly changing settings:

1. Is the network interface up and does it have an address?
2. Is there a route to the target?
3. Is the VPN route present if the lab needs a VPN?
4. Can I reach the gateway?
5. Does DNS resolve, if I'm using a hostname?
6. Is the target service listening, and could ICMP simply be blocked?

I ran into this kind of confusion with a lab VPN: the interface being UP did not by itself prove the target route was correct. A failed ping alone doesn't prove the host is offline.

## Subnetting reminder

A normal IPv4 /24 has 256 addresses in total, usually 254 usable host addresses. A /26 has 64 addresses in total. Network and broadcast addresses are not normally assigned to hosts.

## Next practice

Check my own interface and route table, then explain which route would be used for a local destination and for an internet destination.
