# Late Writeup

## Enumeration

Target host: 10.10.11.156
Performed portscan on target with command: rustscan -a 10.10.11.156 -- -sV -sC -A

```go
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/nath/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.11.156:22
Open 10.10.11.156:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.10.11.156
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-07 23:57 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:57
Completed NSE at 23:57, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:57
Completed NSE at 23:57, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:57
Completed NSE at 23:57, 0.00s elapsed
Initiating Ping Scan at 23:57
Scanning 10.10.11.156 [2 ports]
Completed Ping Scan at 23:57, 0.54s elapsed (1 total hosts)
Initiating Connect Scan at 23:57
Scanning late.htb (10.10.11.156) [2 ports]
Discovered open port 80/tcp on 10.10.11.156
Discovered open port 22/tcp on 10.10.11.156
Completed Connect Scan at 23:57, 0.53s elapsed (2 total ports)
Initiating Service scan at 23:57
Scanning 2 services on late.htb (10.10.11.156)
Completed Service scan at 23:57, 6.74s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.11.156.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:57
Completed NSE at 23:58, 11.89s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:58
Completed NSE at 23:58, 1.58s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:58
Completed NSE at 23:58, 0.00s elapsed
Nmap scan report for late.htb (10.10.11.156)
Host is up, received syn-ack (0.51s latency).
Scanned at 2023-04-07 23:57:52 AEST for 21s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 02:5e:29:0e:a3:af:4e:72:9d:a4:fe:0d:cb:5d:83:07 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDSqIcUZeMzG+QAl/4uYzsU98davIPkVzDmzTPOmMONUsYleBjGVwAyLHsZHhgsJqM9lmxXkb8hT4ZTTa1azg4JsLwX1xKa8m+RnXwJ1DibEMNAO0vzaEBMsOOhFRwm5IcoDR0gOONsYYfz18pafMpaocitjw8mURa+YeY21EpF6cKSOCjkVWa6yB+GT8mOcTZOZStRXYosrOqz5w7hG+20RY8OYwBXJ2Ags6HJz3sqsyT80FMoHeGAUmu+LUJnyrW5foozKgxXhyOPszMvqosbrcrsG3ic3yhjSYKWCJO/Oxc76WUdUAlcGxbtD9U5jL+LY2ZCOPva1+/kznK8FhQN
|   256 41:e1:fe:03:a5:c7:97:c4:d5:16:77:f3:41:0c:e9:fb (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBMen7Mjv8J63UQbISZ3Yju+a8dgXFwVLgKeTxgRc7W+k33OZaOqWBctKs8hIbaOehzMRsU7ugP6zIvYb25Kylw=
|   256 28:39:46:98:17:1e:46:1a:1e:a1:ab:3b:9a:57:70:48 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIGrWbMoMH87K09rDrkUvPUJ/ZpNAwHiUB66a/FKHWrj
80/tcp open  http    syn-ack nginx 1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 1575FDF0E164C3DB0739CF05D9315BDF
|_http-title: Late - Best online image tools
| http-methods: 
|_  Supported Methods: GET HEAD
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 23:58
Completed NSE at 23:58, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 23:58
Completed NSE at 23:58, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 23:58
Completed NSE at 23:58, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.20 seconds
```

Browsing to the http server displays the following page.
![1](assets/1.png)

As the front page talks about a photo editing tool that the user does not hae access to through the normal UI, there is a high chance that this server has a subdomain in which the tool can be accessed.

