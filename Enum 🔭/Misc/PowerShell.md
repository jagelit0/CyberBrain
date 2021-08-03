[Approved Verbs for PowerShell Commands](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7)

Format of a cmdlet -> "Verb-Noun" -> ```Get-Command``` 

* Common Verbs
	* Get
	 * Start
	* Stop 
	* Read
	* Write
	* New
	* Out

To display help inf. ```Get-Help Command-Name``` and ```Get-Help Command-Name -examples```

# Enum w/ PowerShell
```powershell
PS> Get-LocalUser		# Get Users on the machine

PS> Get-LocalUser -SID "S-1-5-21-1394777289-3961777894-1791813945-501"		# Get name of a user by SID

PS> Get-LocalUser | Where-Object -Property PasswordRequired -Match false		# Get password value set to False

PS> Get-LocalGroup		# Enumare groups on the machine

PS> Get-NetIPAddress		# Get IP

PS> Get-NetTCPConnection		# Ports TCP Listening 

PS> Get-Process		#Get All Processes


PS> 

PS>
```