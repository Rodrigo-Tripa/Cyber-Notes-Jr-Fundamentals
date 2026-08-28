# Networking Cheat Sheet

## Interface Information

```bash
ip addr
ip link
ip -br addr

ifconfig
```

Show routing information:

```bash
ip route
route -n
```

Show ARP/neighbor information:

```bash
ip neigh
arp -a
```

## Connectivity

```bash
ping <host>
ping -c 4 <host>

traceroute <host>
tracepath <host>
```

## DNS

```bash
dig example.com
dig A example.com
dig AAAA example.com
dig MX example.com
dig NS example.com
dig TXT example.com

nslookup example.com
host example.com
```

Reverse DNS:

```bash
dig -x <IP>
```

## Sockets and Ports

List listening TCP/UDP sockets:

```bash
ss -tuln
```

Show processes associated with sockets:

```bash
ss -tulnp
```

Show established connections:

```bash
ss -tun
```

Legacy alternative:

```bash
netstat -tulnp
```

## HTTP

Request a URL:

```bash
curl http://example.com
curl https://example.com
```

Show response headers:

```bash
curl -I https://example.com
```

Verbose request:

```bash
curl -v https://example.com
```

Send data:

```bash
curl -X POST -d "key=value" https://example.com
```

Download a resource:

```bash
wget https://example.com/file
```

## TCP / UDP Testing

Test whether a TCP port is reachable:

```bash
nc -vz <host> <port>
```

Connect to a service:

```bash
nc <host> <port>
```

Listen on a TCP port:

```bash
nc -lvnp <port>
```

## Nmap

Basic host scan:

```bash
nmap <target>
```

Service and version detection:

```bash
nmap -sV <target>
```

Default scripts:

```bash
nmap -sC <target>
```

OS detection:

```bash
nmap -O <target>
```

Aggressive scan:

```bash
nmap -A <target>
```

Scan all TCP ports:

```bash
nmap -p- <target>
```

Specific ports:

```bash
nmap -p 22,80,443 <target>
```

UDP scan:

```bash
nmap -sU <target>
```

## Packet Capture

Capture traffic on an interface:

```bash
sudo tcpdump -i eth0
```

Capture a specific host:

```bash
sudo tcpdump -i eth0 host <IP>
```

Capture a specific port:

```bash
sudo tcpdump -i eth0 port 80
```

Read a capture file:

```bash
tcpdump -r capture.pcap
```

List available interfaces:

```bash
tcpdump -D
```

## Common Ports

|  Port | Protocol | Common Service       |
| ----: | -------- | -------------------- |
|    20 | TCP      | FTP Data             |
|    21 | TCP      | FTP                  |
|    22 | TCP      | SSH                  |
|    23 | TCP      | Telnet               |
|    25 | TCP      | SMTP                 |
|    53 | TCP/UDP  | DNS                  |
| 67/68 | UDP      | DHCP                 |
|    80 | TCP      | HTTP                 |
|   110 | TCP      | POP3                 |
|   123 | UDP      | NTP                  |
|   135 | TCP      | MSRPC                |
|   139 | TCP      | NetBIOS              |
|   143 | TCP      | IMAP                 |
|   161 | UDP      | SNMP                 |
|   389 | TCP/UDP  | LDAP                 |
|   443 | TCP      | HTTPS                |
|   445 | TCP      | SMB                  |
|   636 | TCP      | LDAPS                |
|   993 | TCP      | IMAPS                |
|   995 | TCP      | POP3S                |
|  1433 | TCP      | Microsoft SQL Server |
|  3306 | TCP      | MySQL                |
|  3389 | TCP      | RDP                  |
|  5432 | TCP      | PostgreSQL           |
|  5900 | TCP      | VNC                  |
|  8080 | TCP      | HTTP Alternate       |

## Addressing

Private IPv4 ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Loopback:

```text
127.0.0.0/8
127.0.0.1 = localhost
```

IPv4 localhost:

```text
127.0.0.1
```

## CIDR Quick Reference

```text
/8   = 255.0.0.0
/16  = 255.255.0.0
/24  = 255.255.255.0
/25  = 255.255.255.128
/26  = 255.255.255.192
/27  = 255.255.255.224
/28  = 255.255.255.240
/29  = 255.255.255.248
/30  = 255.255.255.252
```

## Useful Network Files

```text
/etc/hosts
/etc/resolv.conf
/etc/hostname
/etc/nsswitch.conf
```

## Routing

View routing table:

```bash
ip route
```

Add a route:

```bash
sudo ip route add <network>/<prefix> via <gateway>
```

Delete a route:

```bash
sudo ip route del <network>/<prefix>
```

## Network Discovery

Basic host discovery with Nmap:

```bash
nmap -sn <network>/<prefix>
```

Example:

```bash
nmap -sn 192.168.1.0/24
```

## Useful Troubleshooting Sequence

```text
1. Check interface
2. Check IP address
3. Check routing table
4. Test local gateway
5. Test external IP
6. Test DNS resolution
7. Test application/service
```

Typical commands:

```bash
ip addr
ip route
ping <gateway>
ping 1.1.1.1
dig example.com
curl https://example.com
```
