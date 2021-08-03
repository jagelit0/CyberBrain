## LDAP Enum.
```bash
ldapsearch -x -h lightweight.htb -b "dc=lightweight,dc=htb"

-x : simple authentication
-h : LDAP server
-b : base dn for search
```

```bash
ldapsearch -x -h <IP> -D '<DOMAIN>\<username>' -w '<password>' -b "DC=<1_SUBDOMAIN>,DC=<TDL>"

-x : Simple Authentication
-h : LDAP Server
-D : My User
-w : My password
-b : Base site, all data from here will be given
```
### Nmap Script
```bash
nmap --script=ldap-search lightweight.htb
```
---
