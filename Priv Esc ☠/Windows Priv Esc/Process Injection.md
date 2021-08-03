## PowerShell commands
```powershell
PS > ps | findstr firefox
```

## procdump.exe
https://docs.microsoft.com/en-us/sysinternals/downloads/procdump
```powershell
PS > ./procdump64.exe -accepteula (first time)
PS > ./procdump64.exe -ma (PROCESS ID)
```