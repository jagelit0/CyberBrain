# Ffuf
## Simple file discover: 
```bash
ffuf -b " COOKIE " -w /root/wordlists/common.txt -u https://example.com/FUZZ
```

## Proxifiying ffuf traffic
```bash
$ ffuf -u http://MACHINE_IP/ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -x http://127.0.0.1:8080
$ ffuf -u http://MACHINE_IP/ -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -replay-proxy http://127.0.0.1:8080
```