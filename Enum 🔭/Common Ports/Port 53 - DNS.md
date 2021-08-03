### Resources: 
* https://book.hacktricks.xyz/pentesting/pentesting-dns
* https://www.exploit-db.com/docs/13687
## Nmap script
--script dns-nsid

## Zone Transfer
```bash

$ dig axfr @DNS-IP #Zone Transfer without domain

$ dig axfr @DNS-IP DOMAIN #Zone Transfer guessing domain

$ fierce -dns DOMAIN
```

## Dig
```bash
$ dig ANY @<DNS\_IP\> <DOMAIN\> #Any information

$ dig A @<DNS\_IP\> <DOMAIN\> #Regular DNS request

$ dig AAAA @<DNS\_IP\> <DOMAIN\> #IPv6 DNS request

$ dig TXT @<DNS\_IP\> <DOMAIN\> #Information

$ dig MX @<DNS\_IP\> <DOMAIN\> #Emails related

$ dig NS @<DNS\_IP\> <DOMAIN\> #DNS that resolves that name

$ dig -x 192.168.0.2 @<DNS\_IP\> #Reverse lookup

$ dig -x 2a00:1450:400c:c06::93 @<DNS\_IP\> #reverse IPv6 lookup

$ dig @10.13.37.10 -x 10.13.37.10

#Use \[-p PORT\] or -6 (to use ivp6 address of dns)
```

## Nslookup
```bash
nslookup
$ SERVER <IP\_DNS\> #Select dns server

$ 127.0.0.1 #Reverse lookup of 127.0.0.1, maybe...

$ <IP\_MACHINE\> #Reverse lookup of a machine, maybe...
```