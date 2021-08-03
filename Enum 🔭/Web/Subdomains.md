# Sublist3r
* Query various search engines looking for SSL certificates, etc.:
```bash
sublist3r -d example.com
```


# Dnsrecon
* Search possible subdomains with a wordlist :
```bash
dnsrecon -d example.com -D /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -t brt
```

# Gobuster
```bash
$ gobuster vhost -u http://schooled.htb -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -o subdomains.txt -t 40
```


# Fuff
```bash
$ ffuf -c -u http://rocket.thm -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H 'Host: FUZZ.rocket.thm' -fw 20 -mc all
$ ffuf -u http://FUZZ.mydomain.com -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 0
$ ffuf -u http://mydomain.com -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H 'Host: FUZZ.mydomain.com' -fs 0
```