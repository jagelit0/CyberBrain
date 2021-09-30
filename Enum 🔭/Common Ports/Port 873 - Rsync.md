
**rsync** is a utility for efficiently [transferring](https://en.wikipedia.org/wiki/File_transfer) and [synchronizing](https://en.wikipedia.org/wiki/File_synchronization) [files](https://en.wikipedia.org/wiki/Computer_file) between a computer and an external hard drive and across [networked](https://en.wikipedia.org/wiki/Computer_network) [computers](https://en.wikipedia.org/wiki/Computer) by comparing the [modification times](https://en.wikipedia.org/wiki/Timestamping_(computing))and sizes of files. It is commonly found on [Unix-like](https://en.wikipedia.org/wiki/Unix-like) [operating systems](https://en.wikipedia.org/wiki/Operating_system). The rsync algorithm is a type of [delta encoding](https://en.wikipedia.org/wiki/Delta_encoding), and is used for minimizing network usage. [Zlib](https://en.wikipedia.org/wiki/Zlib) may be used for additional [data compression](https://en.wikipedia.org/wiki/Data_compression), and [SSH](https://en.wikipedia.org/wiki/Secure_Shell) or [stunnel](https://en.wikipedia.org/wiki/Stunnel) can be used for security.

---
# Enumeration
## Manual
```bash
jagelito ~$ nc -vn 10.10.170.253 873
(UNKNOWN) [10.10.170.253] 873 (rsync) open
@RSYNCD: 31.0				# VERSION FROM THE SERVER
@RSYNCD: 31.0				# THEN YOU SEND THE SAME INFO
#list						# THEN YOU ASK THE SERVER TO LIST
Conf            All Confs	# SHARES
@RSYNCD: EXIT				# SERVER CLOSE CONNECTION
```

## Nmap
```bash
$ nmap -sC --script "rsync-list-modules" -p873 10.10.170.253
PORT    STATE SERVICE
873/tcp open  rsync
| rsync-list-modules: 
|_  Conf                All Confs
```

## MSF
```bash
msf> use auxiliary/scanner/rsync/modules_list
```

# List Shares

## rsync
Enumerate all shares
```bash
$ rsync -av --list-only rsync://10.10.170.253/Conf
receiving incremental file list
drwxrwxrwx          4,096 2021/04/10 22:03:08 .
-rw-r--r--          4,620 2021/04/09 22:01:22 access.conf
-rw-r--r--          1,341 2021/04/09 21:56:12 bluezone.ini
-rw-r--r--          2,969 2021/04/09 22:02:24 debconf.conf
-rw-r--r--            332 2021/04/09 22:01:38 ldap.conf
-rw-r--r--         94,404 2021/04/09 22:21:57 lvm.conf
-rw-r--r--          9,005 2021/04/09 21:58:40 mysql.ini
-rw-r--r--         70,207 2021/04/09 21:56:56 php.ini
-rw-r--r--            320 2021/04/09 22:03:16 ports.conf
-rw-r--r--            589 2021/04/09 22:01:07 resolv.conf
-rw-r--r--             29 2021/04/09 22:02:56 screen-cleanup.conf
-rw-r--r--          9,542 2021/04/09 22:00:59 smb.conf
-rw-rw-r--             72 2021/04/10 22:03:06 webapp.ini
```

Copy shares to local machine
```bash
$ rsync -av rsync://10.10.170.253/Conf ./rsync_share
receiving incremental file list
created directory ./rsync_share
./
access.conf
bluezone.ini
debconf.conf
ldap.conf
lvm.conf
mysql.ini
php.ini
ports.conf
resolv.conf
screen-cleanup.conf
smb.conf
webapp.ini
```


# Transfer files
```bash
jagelito ~$ rsync -av /home/jagelito/Ctf/thm/meta/content/rsync/rsync_shares/webapp.ini rsync://10.10.170.253/Conf/webapp.ini
sending incremental file list
webapp.ini

sent 187 bytes  received 41 bytes  456.00 bytes/sec
total size is 71  speedup is 0.31
```










## Resources
* https://book.hacktricks.xyz/pentesting/873-pentesting-rsync