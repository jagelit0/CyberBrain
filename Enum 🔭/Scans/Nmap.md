# Nmap Scanings
---
## Initial Scanings
```bash
nmap -p- --open --min-rate 5000 (optional) (IP) 
nmap -sU --min-rate 5000 (IP)
nmap -sT -p- -v --min-rate 5000 (IP)
```
## Deep Scanings
```bash
nmap -sC -sV -T5 -p(ports to scan) (IP)
nmap -A -sC -sV -v -T4 -p(ports to scan) (IP)
nmap -sU -p(ports to scan) -sV -sC (IP) --min-rate 500 
```