### [ENUMERATION]
          └─$ nmap 10.10.10.4 -Pn --version-light -sV -A
          Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
          Starting Nmap 7.91 ( https://nmap.org ) at 2021-02-05 15:21 EST
          Nmap scan report for 10.10.10.4
          Host is up (0.041s latency).
          Not shown: 997 filtered ports
          PORT     STATE  SERVICE       VERSION
          139/tcp  open   netbios-ssn   Microsoft Windows netbios-ssn
          445/tcp  open   microsoft-ds  Windows XP microsoft-ds
          3389/tcp closed ms-wbt-server
          Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

          Host script results:
          |_clock-skew: mean: -3h55m55s, deviation: 1h24m50s, median: -4h55m55s
          |_nbstat: NetBIOS name: LEGACY, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:b9:3c:69 (VMware)
          | smb-os-discovery: 
          |   OS: Windows XP (Windows 2000 LAN Manager)
          |   OS CPE: cpe:/o:microsoft:windows_xp::-
          |   Computer name: legacy
          |   NetBIOS computer name: LEGACY\x00
          |   Workgroup: HTB\x00
          |_  System time: 2021-02-05T19:25:26+02:00
          | smb-security-mode: 
          |   account_used: guest
          |   authentication_level: user
          |   challenge_response: supported
          |_  message_signing: disabled (dangerous, but default)
          |_smb2-time: Protocol negotiation failed (SMB2)

          └─$ nmap -vvvvv -A -sVT 10.10.10.4 -Pn


          Reason: 997 no-responses
          PORT     STATE  SERVICE       REASON       VERSION
          139/tcp  open   netbios-ssn   syn-ack      Microsoft Windows netbios-ssn
          445/tcp  open   microsoft-ds  syn-ack      Windows XP microsoft-ds
          3389/tcp closed ms-wbt-server conn-refused
          Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

          Host script results:
          |_clock-skew: mean: -3h55m53s, deviation: 1h24m51s, median: -4h55m53s
          | nbstat: NetBIOS name: LEGACY, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:b9:3c:69 (VMware)
          | Names:
          |   LEGACY<00>           Flags: <unique><active>
          |   HTB<00>              Flags: <group><active>
          |   LEGACY<20>           Flags: <unique><active>
          |   HTB<1e>              Flags: <group><active>
          |   HTB<1d>              Flags: <unique><active>
          |   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
          | Statistics:
          |   00 50 56 b9 3c 69 00 00 00 00 00 00 00 00 00 00 00
          |   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
          |_  00 00 00 00 00 00 00 00 00 00 00 00 00 00
          | p2p-conficker: 
          |   Checking for Conficker.C or higher...
          |   Check 1 (port 40600/tcp): CLEAN (Timeout)
          |   Check 2 (port 40867/tcp): CLEAN (Timeout)
          |   Check 3 (port 50902/udp): CLEAN (Timeout)
          |   Check 4 (port 25839/udp): CLEAN (Timeout)
          |_  0/4 checks are positive: Host is CLEAN or ports are blocked
          | smb-os-discovery: 
          |   OS: Windows XP (Windows 2000 LAN Manager)
          |   OS CPE: cpe:/o:microsoft:windows_xp::-
          |   Computer name: legacy
          |   NetBIOS computer name: LEGACY\x00
          |   Workgroup: HTB\x00
          |_  System time: 2021-02-06T14:51:42+02:00
          | smb-security-mode: 
          |   account_used: guest
          |   authentication_level: user
          |   challenge_response: supported
          |_  message_signing: disabled (dangerous, but default)
          |_smb2-security-mode: Couldn't establish a SMBv2 connection.
          |_smb2-time: Protocol negotiation failed (SMB2)

          NSE: Script Post-scanning.
          NSE: Starting runlevel 1 (of 3) scan.
          Initiating NSE at 10:48
          Completed NSE at 10:48, 0.00s elapsed
          NSE: Starting runlevel 2 (of 3) scan.
          Initiating NSE at 10:48
          Completed NSE at 10:48, 0.00s elapsed
          NSE: Starting runlevel 3 (of 3) scan.
          Initiating NSE at 10:48
          Completed NSE at 10:48, 0.00s elapsed
          Read data files from: /usr/bin/../share/nmap
          Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
          Nmap done: 1 IP address (1 host up) scanned in 61.77 seconds

### [ANALYSIS]
    #SMB on XP means 08-067
    Searchsploit on it
    SMB exploit could attempt with python script or smbclient attack


    searched on msfconsole 
    reset box due to issues
    ** ensure msfconsole is  run as root
    *** ensure set ip to tun0(htb openvpn) versus briged ip auto generated

### [Exploit/Payload}
    windows/smb/ms08_067_netapi
    set target to 6 as it did not work before with auto target

### [Hashes]
    User hash found in User's desktop C:\Documents and Settings\John\Desktop\user.txt
    Root has found in admin desktop C:\Documents and Settings\Administrator\Desktop\root.txt
