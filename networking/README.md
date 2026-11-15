# Networking for Cybersecurity

## Essential concepts

- **IP address:** logical address used to identify an interface on an IP network.
- **Subnet mask / prefix:** identifies the network portion of an address.
- **Default gateway:** router used to reach destinations outside the local subnet.
- **DNS:** resolves names to records such as A, AAAA, and MX.
- **DHCP:** leases network configuration to clients.
- **MAC address:** link-layer identifier used on a local network.

## TCP and UDP

TCP is connection-oriented and provides ordered, reliable byte-stream delivery. UDP is connectionless and has lower protocol overhead but does not guarantee delivery or ordering.

## Common ports

| Port | Common service | Transport |
|---:|---|---|
| 20/21 | FTP data/control | TCP |
| 22 | SSH | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | UDP/TCP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |
| 123 | NTP | UDP |
| 143 | IMAP | TCP |
| 443 | HTTPS | TCP |
| 445 | SMB | TCP |
| 3306 | MySQL | TCP |
| 3389 | RDP | TCP |

A port number alone does not prove which application is running. Verify with service detection and context.

## Useful Linux commands

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

## Troubleshooting sequence

1. Check interface state and assigned address.
2. Check route and default gateway.
3. Test the gateway.
4. Test a public IP to separate routing from DNS.
5. Test DNS resolution.
6. Check VPN routes, firewall rules, and service availability.

A failed ping does not automatically mean a host is offline; ICMP may be filtered.

## Subnetting reminder

For IPv4, a /24 has 256 total addresses (traditionally 254 usable host addresses in a conventional subnet). A /26 has 64 total addresses. Network and broadcast address rules apply to ordinary IPv4 subnets.

## Practice

In an authorized lab, inspect your own interface and route table. Explain which route would be selected for a destination inside your LAN and for an internet destination.
