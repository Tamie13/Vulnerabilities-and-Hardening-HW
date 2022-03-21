# Web Vulnerabilities And Hardening
(Cybersecurity Bootcamp Unit 15 Assignment)

### Topics Covered Will Include:
- Web application vulnerability assessments
- Injection
- Brute force attacks
- Broken authentication
- Burp Suite
- Web proxies
- Directory traversal
- Dot dot slash attacks
- Beef
- Cross-site scripting
- Malicious payloads

### Content will include steps on how to test the vulnerabilities of a web application using a virtual machine.  
Steps will include:  

- Detailing how to setup and access the applications
- A walkthrough of how the application is intended to work
- Task that will test the application for vulnerabilities

### To launch the environment with several vulnerable web applications, complete the following:

Use the command line to run Vagrant with the following command: 
- vagrant up

### Then, open terminal inside Vagrant and run the following on the command line: 
- cd ./Documents/web-vulns && docker-compose up

While the output might look like the task is still running, this script has launched several vulnerable web applications that we will use throughout this assignment.  Leave this page open and running then open a another terminal window to be used later.

Next open your browser and navigate to:

http://192.168.13.25

- Login credentials:

    * User Name: admin
    * Password:  password

**Next Select:** 

*Command Injection*
option (See image below)

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/command%20injection%20shot.png)

      This page is a new web application built by Replicants in order to enable their customers to ping an IP address. 
      The web page will return the results of the ping command back to the user.  You will run a series of commands 
      to walkthrough the intended purpose of the web application.
      
      
**Command One**
Test the webpage start by entering the IP address 
`8.8.8.8`
and press submit to see the results display on the web application.

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Ping%208.8.8.8.png)

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Results%20of%20Ping%20of%208.8.8.8.png)

  - Behind the scenes, when you select Submit, the IP you type in the field is injected into a command that is run against the Replicants webserver. The specific command     that ran on the webserver is ping <IP> and 8.8.8.8 is the field value that is injected into that command.
   
   
**Command Two**
Test Replicant webserver to see if it can be manipulated by inputing a different payload in the field by
`Typing: 8.8.8.8 && pwd`
   
![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/PWD%20Results.png)
   

