Ports  25,465,587

### Banner Grabbing/Basic connection
SMTP:
```bash
$ nc -vn <IP> 25
```

SMTPS:
```bash
$ openssl s\_client -crlf -connect smtp.mailgun.org:465 #SSL/TLS without starttls command

$ openssl s\_client -starttls smtp -crlf -connect smtp.mailgun.org:587
```

### Nmap
```bash
$ nmap -p25 --script smtp-commands 10.10.10.10
```

### Metasploit
#### User enum:
```bash
$ user auxiliary/scanner/smtp/smtp_enum
```


### ISMTP
```bash
$ 
```