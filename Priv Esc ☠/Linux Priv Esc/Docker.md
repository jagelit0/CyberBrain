# Linux
## Version
```bash
$ docker --version
	Docker version 18.06.0-ce, build 0ffa825	# Vulnerable example
	
$ sudo -l
	User noah may run the following commands on thenotebook:
    	(ALL) NOPASSWD: /usr/bin/docker exec -it webapp-dev01*
```
Then, check for exploits \#Example above [EXPLOIT PRIV ESC](https://github.com/Frichetten/CVE-2019-5736-PoC#cve-2019-5736-poc)


## CAPABLITIES
https://blog.pentesteracademy.com/abusing-sys-module-capability-to-perform-docker-container-breakout-cf5c29956edd
**VULNERABLE CAP. -> sys\_module**


## Other resources
https://gtfobins.github.io/gtfobins/docker/
https://keiran.scot/privilege-escallation-with-docker-56dc682a6e17
https://book.hacktricks.xyz/linux-unix/privilege-escalation/docker-breakout