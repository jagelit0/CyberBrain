https://steflan-security.com/smb-enumeration-guide
https://www.hackingarticles.in/a-little-guide-to-smb-enumeration/
## smbmap
```bash
$ smbmap -H IP
```

## smbclient
```bash
$ smbclient -N \\\\IP\\FILE
```

## smbget
```bash
$ smbget -a -R smb://domain.local/Backups . ( -a : Guest )
```

## Mounting SMB Folders
```bash
mount -t cifs //bastion.htb/Backups /mnt/bastion
```

## rpcclient
https://www.hackingarticles.in/active-directory-enumeration-rpcclient/

```bash
$ rpcclient -U "" -N 10.10.10.149 (Null session)
$ rppclient $> lsaenumsid
```

```bash
			OTHER WAY TO ENUMERATE SID (impacket)
$ python3 lookupsid.py hazard:stealth1agent@10.10.10.149
```

```bash
rpcclient $> querydominfo				# Domain Inf.

rpcclient $> srvinfo					# Server Inf.

rpcclient $> enumdomusers				# Enum Domain Users.
rpcclient $> queryuser alice			# User Queries.

rpcclient $> enumdomgroups				# Enum Domain Groups.
rpcclient $> querygroup 0x200			# Group Queries.

rpcclient $> enumprivs					# Enum. Privileges.

rpcclient $> getdompwinfo				# Domain Password Inf.

rpcclient $> lsaenumsid					# Enum. SID from LSA.

rpcclient $> netshareenum				# Net Share Enum.
rpcclient $> netshareenumall
rpcclient $> netsharegetinfo Backup		# Net Share Get Inf.
rpcclient $>
```