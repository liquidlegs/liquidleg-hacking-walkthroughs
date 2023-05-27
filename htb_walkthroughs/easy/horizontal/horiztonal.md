# Horizontal Writeup

![intro](assets/intro.png)

TCP portscan
```php
┌─[nath@parrot]─[~/pentesting/htb/vpn/us]
└──╼ $rustscan -a 10.10.11.105 -p 22,80 -- -sV -sC -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/nath/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.11.105:80
Open 10.10.11.105:22
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.10.11.105
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-28 22:46 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:46
Completed NSE at 22:46, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:46
Completed NSE at 22:46, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:46
Completed NSE at 22:46, 0.00s elapsed
Initiating Ping Scan at 22:46
Scanning 10.10.11.105 [2 ports]
Completed Ping Scan at 22:46, 0.25s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:46
Completed Parallel DNS resolution of 1 host. at 22:46, 0.04s elapsed
DNS resolution of 1 IPs took 0.04s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 22:46
Scanning 10.10.11.105 [2 ports]
Discovered open port 80/tcp on 10.10.11.105
Discovered open port 22/tcp on 10.10.11.105
Completed Connect Scan at 22:46, 0.51s elapsed (2 total ports)
Initiating Service scan at 22:46
Scanning 2 services on 10.10.11.105
Completed Service scan at 22:46, 7.10s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.105.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:46
Completed NSE at 22:47, 13.70s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:47
Completed NSE at 22:47, 2.34s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:47
Completed NSE at 22:47, 0.00s elapsed
Nmap scan report for 10.10.11.105
Host is up, received syn-ack (0.31s latency).
Scanned at 2023-04-28 22:46:47 AEST for 24s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ee:77:41:43:d4:82:bd:3e:6e:6e:50:cd:ff:6b:0d:d5 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL2qJTqj1aoxBGb8yWIN4UJwFs4/UgDEutp3aiL2/6yV2iE78YjGzfU74VKlTRvJZWBwDmIOosOBNl9nfmEzXerD0g5lD5SporBx06eWX/XP2sQSEKbsqkr7Qb4ncvU8CvDR6yGHxmBT8WGgaQsA2ViVjiqAdlUDmLoT2qA3GeLBQgS41e+TysTpzWlY7z/rf/u0uj/C3kbixSB/upkWoqGyorDtFoaGGvWet/q7j5Tq061MaR6cM2CrYcQxxnPy4LqFE3MouLklBXfmNovryI0qVFMki7Cc3hfXz6BmKppCzMUPs8VgtNgdcGywIU/Nq1aiGQfATneqDD2GBXLjzV
|   256 3a:d5:89:d5:da:95:59:d9:df:01:68:37:ca:d5:10:b0 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBIyw6WbPVzY28EbBOZ4zWcikpu/CPcklbTUwvrPou4dCG4koataOo/RDg4MJuQP+sR937/ugmINBJNsYC8F7jN0=
|   256 4a:00:04:b4:9d:29:e7:af:37:16:1b:4f:80:2d:98:94 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJqmDVbv9RjhlUzOMmw3SrGPaiDBgdZ9QZ2cKM49jzYB
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
|_http-title: Did not follow redirect to http://horizontall.htb
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: nginx/1.14.0 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 22:47
Completed NSE at 22:47, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 22:47
Completed NSE at 22:47, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 22:47
Completed NSE at 22:47, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.13 seconds
```

Server technologies analyzed web webappalyzer.
![1](assets/1.png)

Admin password `$2a$10$p4Q9jUcPi5PdHlv0csRBYeyY.97vcDKHmD1imRmRVUL3qO5mAqcLS`
New admin password `SuperStrongPassword1`