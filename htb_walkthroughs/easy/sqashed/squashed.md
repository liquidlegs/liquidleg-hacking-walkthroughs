# Squashed Writeup

## Enumeration

Target host: 10.10.11.191
Performed port scan on target with ./rustscan -a 10.10.11.191 -- -sV -sC -A

```go
[~] The config file is expected to be at "/home/nath/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.11.191:22
Open 10.10.11.191:80
Open 10.10.11.191:111
Open 10.10.11.191:2049
Open 10.10.11.191:8000
Open 10.10.11.191:33651
Open 10.10.11.191:43089
Open 10.10.11.191:45483
Open 10.10.11.191:60331
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.10.11.191
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-07 14:47 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:47
Completed NSE at 14:47, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:47
Completed NSE at 14:47, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:47
Completed NSE at 14:47, 0.00s elapsed
Initiating Ping Scan at 14:47
Scanning 10.10.11.191 [2 ports]
Completed Ping Scan at 14:47, 0.29s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 14:47
Completed Parallel DNS resolution of 1 host. at 14:47, 0.05s elapsed
DNS resolution of 1 IPs took 0.05s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 14:47
Scanning 10.10.11.191 [9 ports]
Discovered open port 22/tcp on 10.10.11.191
Discovered open port 80/tcp on 10.10.11.191
Discovered open port 111/tcp on 10.10.11.191
Discovered open port 8000/tcp on 10.10.11.191
Discovered open port 43089/tcp on 10.10.11.191
Discovered open port 33651/tcp on 10.10.11.191
Discovered open port 45483/tcp on 10.10.11.191
Discovered open port 2049/tcp on 10.10.11.191
Discovered open port 60331/tcp on 10.10.11.191
Completed Connect Scan at 14:47, 0.46s elapsed (9 total ports)
Initiating Service scan at 14:47
Scanning 9 services on 10.10.11.191
Completed Service scan at 14:47, 10.65s elapsed (9 services on 1 host)
NSE: Script scanning 10.10.11.191.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:47
Completed NSE at 14:48, 11.54s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:48
Completed NSE at 14:48, 1.53s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:48
Completed NSE at 14:48, 0.00s elapsed
Nmap scan report for 10.10.11.191
Host is up, received syn-ack (0.40s latency).
Scanned at 2023-04-07 14:47:45 AEST for 25s

PORT      STATE SERVICE  REASON  VERSION
22/tcp    open  ssh      syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC82vTuN1hMqiqUfN+Lwih4g8rSJjaMjDQdhfdT8vEQ67urtQIyPszlNtkCDn6MNcBfibD/7Zz4r8lr1iNe/Afk6LJqTt3OWewzS2a1TpCrEbvoileYAl/Feya5PfbZ8mv77+MWEA+kT0pAw1xW9bpkhYCGkJQm9OYdcsEEg1i+kQ/ng3+GaFrGJjxqYaW1LXyXN1f7j9xG2f27rKEZoRO/9HOH9Y+5ru184QQXjW/ir+lEJ7xTwQA5U1GOW1m/AgpHIfI5j9aDfT/r4QMe+au+2yPotnOGBBJBz3ef+fQzj/Cq7OGRR96ZBfJ3i00B/Waw/RI19qd7+ybNXF/gBzptEYXujySQZSu92Dwi23itxJBolE6hpQ2uYVA8VBlF0KXESt3ZJVWSAsU3oguNCXtY7krjqPe6BZRy+lrbeska1bIGPZrqLEgptpKhz14UaOcH9/vpMYFdSKr24aMXvZBDK1GJg50yihZx8I9I367z0my8E89+TnjGFY2QTzxmbmU=
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBH2y17GUe6keBxOcBGNkWsliFwTRwUtQB3NXEhTAFLziGDfCgBV7B9Hp6GQMPGQXqMk7nnveA8vUz0D7ug5n04A=
|   256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKfXa+OM5/utlol5mJajysEsV4zb/L0BJ1lKxMPadPvR
80/tcp    open  http     syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-title: Built Better
|_http-server-header: Apache/2.4.41 (Ubuntu)
111/tcp   open  rpcbind  syn-ack 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      33911/tcp6  mountd
|   100005  1,2,3      36572/udp6  mountd
|   100005  1,2,3      43125/udp   mountd
|   100005  1,2,3      60331/tcp   mountd
|   100021  1,3,4      33842/udp6  nlockmgr
|   100021  1,3,4      35156/udp   nlockmgr
|   100021  1,3,4      35627/tcp6  nlockmgr
|   100021  1,3,4      43089/tcp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs_acl  syn-ack 3 (RPC #100227)
8000/tcp  open  http     syn-ack SimpleHTTPServer 0.6 (Python 3.8.10)
|_http-title: Directory listing for /
| http-methods: 
|_  Supported Methods: GET HEAD
|_http-server-header: SimpleHTTP/0.6 Python/3.8.10
33651/tcp open  mountd   syn-ack 1-3 (RPC #100005)
43089/tcp open  nlockmgr syn-ack 1-4 (RPC #100021)
45483/tcp open  mountd   syn-ack 1-3 (RPC #100005)
60331/tcp open  mountd   syn-ack 1-3 (RPC #100005)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 14:48
Completed NSE at 14:48, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 14:48
Completed NSE at 14:48, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 14:48
Completed NSE at 14:48, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.34 seconds
```

