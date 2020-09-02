# Jack

## Summary

### Tools Used
* `nmap`, `wpscan`, `python`, `pspy`

## Enum

##### Nmap

`sudo nmap -A jack.thm -oN jack `

`nmap` tells us we have a host running ssh and serving a wordpress application. 

```
# Nmap 7.80 scan initiated Sun Aug 30 03:57:41 2020 as: nmap -A -oN jack -v jack.thm
Nmap scan report for jack.thm (10.10.126.131)
Host is up (0.30s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 3e:79:78:08:93:31:d0:83:7f:e2:bc:b6:14:bf:5d:9b (RSA)
|   256 3a:67:9f:af:7e:66:fa:e3:f8:c7:54:49:63:38:a2:93 (ECDSA)
|_  256 8c:ef:55:b0:23:73:2c:14:09:45:22:ac:84:cb:40:d2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: D41D8CD98F00B204E9800998ECF8427E
|_http-generator: WordPress 5.3.2
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Jack&#039;s Personal Site &#8211; Blog for Jacks writing adven...
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=8/30%OT=22%CT=1%CU=42716%PV=Y%DS=4%DC=T%G=Y%TM=5F4B15C
OS:E%P=x86_64-pc-linux-gnu)SEQ(SP=106%GCD=1%ISR=10A%TI=Z%CI=I%II=I%TS=8)SEQ
OS:(SP=106%GCD=1%ISR=10A%TI=Z%CI=I%TS=8)OPS(O1=M509ST11NW7%O2=M509ST11NW7%O
OS:3=M509NNT11NW7%O4=M509ST11NW7%O5=M509ST11NW7%O6=M509ST11)WIN(W1=68DF%W2=
OS:68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M509NNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Uptime guess: 0.014 days (since Sun Aug 30 03:38:38 2020)
Network Distance: 4 hops
TCP Sequence Prediction: Difficulty=262 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 587/tcp)
HOP RTT       ADDRESS
1   167.61 ms 10.13.0.1
2   ... 3
4   304.95 ms jack.thm (10.10.126.131)

Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Aug 30 03:58:22 2020 -- 1 IP address (1 host up) scanned in 41.89 seconds
```

##### WPScan

`wpscan --url jack.thm`

>XML-RPC seems to be enabled

We can use this to enumerate usernames. Let's try:
* `http://jack.thm/wp-json/wp/v2/users/1` - 200 - we are able to see the *jack* user (that we already know about)
* `http://jack.thm/wp-json/wp/v2/users/2` - 401 - not allowed to view this user
* `http://jack.thm/wp-json/wp/v2/users/99` - 404 - user not found

WPScan to the rescue as it provides user enumerition AND bruteforcing which may allow us into the `wp-admin` panel. We find 2 additional users.

`wpscan --wpscan --url jack.thm --enumerate u`

Put all three users into a users.txt file and use a wordlist of your choice to brute force. We are able to sucesfully obtain a password for a user. Use that to login to `wp-admin`. 

`wpscan --url jack.thm --passwords rockyou.txt --usernames users.txt`

Unfortunately, once logged in, the user does not have any administrative rights. Time to move onto exploitation.

## Exploit


### User

* https://www.exploit-db.com/exploits/44595
* edit plugin php
* insert php reverse shell
* gain access to `www-data` user shell
* obtain user flag

## Priv Esc

Our next aim is to move from `www-data` to `jack`. Fortunately, according to `reminder.txt` in jack's home directory, this user has an issue setting permissions on backups. Doing a quick check we find `/var/backups` that contains some goodies that `www-data` is able to read. Using this, we can SSH to the host. 

`find / -name backup* 2>/dev/null`

## Root

* linPEAS (or any other privesc script of choice)
* nothing of interest can be found apart from various interesting file access rights.
* hint reveals that python is being used.
* use `pspy` to monitor for any strange cronjobs by root
* 👀
    * `2020/08/30 00:26:01 CMD: UID=0    PID=3036   | /usr/bin/python /opt/statuscheck/checker.py `
##### python exploitation

`checker.py`:

```python
import os

os.system("/usr/bin/curl -s -I http://127.0.0.1 >> /opt/statuscheck/output.log")
```

From previous linenum scripts `jack` is a part of `family` which has write access to /usr/lib/python2.7/

Since we know `os.system` is being used in the script we have a lot of options to gain root access such as:

* modify `os.py` to facilitate a reverse shell.
* change permissions of other files and folders within the system (as root).
* change ssh configs to allow for password-less root access via ssh.
* obtain the root flag and write it to a file that is world readable.



{%hackmd theme-dark %}