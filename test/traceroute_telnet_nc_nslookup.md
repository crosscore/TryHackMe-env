```
  780  traceroute 10.10.115.163
  781  telnet 10.10.116.163 80
  782  telnet 10.10.115.163 80
  783  ping -c 1 10.10.115.163
  784  telnet 10.10.115.163 80
  786  nc 10.10.115.163 80
  787  nc 10.10.115.163 21
  789  nc 10.10.58.9 21
  790  telnet google.co.jp 80
  799  whois tryhackme.com
```

```
┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=A tryhackme.com
Server:         192.168.3.1
Address:        192.168.3.1#53

Non-authoritative answer:
Name:   tryhackme.com
Address: 104.22.55.228
Name:   tryhackme.com
Address: 104.22.54.228
Name:   tryhackme.com
Address: 172.67.27.10


┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=AAAA tryhackme.com
Server:         192.168.3.1
Address:        192.168.3.1#53

Non-authoritative answer:
Name:   tryhackme.com
Address: 2606:4700:10::6816:36e4
Name:   tryhackme.com
Address: 2606:4700:10::6816:37e4
Name:   tryhackme.com
Address: 2606:4700:10::ac43:1b0a


┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=A tryhackme.com 1.1.1.1
Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
Name:   tryhackme.com
Address: 172.67.27.10
Name:   tryhackme.com
Address: 104.22.55.228
Name:   tryhackme.com
Address: 104.22.54.228


┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=MX tryhackme.com 1.1.1.1
Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
tryhackme.com   mail exchanger = 1 aspmx.l.google.com.
tryhackme.com   mail exchanger = 10 alt3.aspmx.l.google.com.
tryhackme.com   mail exchanger = 10 alt4.aspmx.l.google.com.
tryhackme.com   mail exchanger = 5 alt1.aspmx.l.google.com.
tryhackme.com   mail exchanger = 5 alt2.aspmx.l.google.com.

Authoritative answers can be found from:


┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=TXT tryhackme.com 1.1.1.1
Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
tryhackme.com   text = "google-site-verification=umR4x8HuzWMF5g3656JY1b-61NuryD0-GqGnYN13ONo"
tryhackme.com   text = "v=spf1 include:_spf.google.com include:email.chargebee.com include:7168674.spf05.hubspotemail.net ~all"

Authoritative answers can be found from:


┌──(yuu㉿kali)-[~/TryHackMe/test]
└─$ nslookup -type=TXT thmlabs.com 1.1.1.1
Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
thmlabs.com     text = "THM{a5b83929888ed36acb0272971e438d78}"

Authoritative answers can be found from:
```
