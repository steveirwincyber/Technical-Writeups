https://tryhackme.com/room/investigatingwindows

### Whats the version and year of the windows machine?
	ver
	systeminfo
		#Windows Server 2016 (Datacenter)
### Which user logged in last?
	wevtutil qe Security /c:30 "/q:*[System [(EventID=4624)]]"
	#outside of system we see Administrator logged in when seaarching under the TargetUserName
### When did John log onto the system last?
	wevtutil qe Security "/q:*[System [(EventID=4624)]]" | findstr "john"
	# 03/02/2019 5:48:32 PM
### What IP does the system connect to when it first starts?

### What two accounts had administrative privileges (other than the Administrator user)?
	net localgroup administrators
### Whats the name of the scheduled task that is malicous.
	schtasks | findstr /C:"Ready" /c:"Running"
	#Clean FIle System
### What file was the task trying to run daily?

### What port did this file listen locally for?

### When did Jenny last logon?
	net user jenny
	#never
### At what date did the compromise take place?

### At what time did Windows first assign special privileges to a new logon?

### What tool was used to get Windows passwords?
	MIM.exe running on desktop and if you click on it shows shell
	#Mimikatz
### What was the attackers external control and command servers IP?

### What was the extension name of the shell uploaded via the servers website?

### What was the last port the attacker opened?

### Check for DNS poisoning, what site was targeted?
	ipconfig /displaydns
	#google shows 76.32.97.132 ip which is not owned by them
	#google.com

