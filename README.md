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

## Web Application Vulnerability One: Command Injection:

Open your browser and navigate to:

http://192.168.13.25

- Login credentials:

    * User Name: admin
    * Password:  password

Next select:
*Command Injection*
option from the menu on the left. (See image below)

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/command%20injection%20shot.png)

      This page is a new web application built by Replicants in order to enable their customers to ping an IP address. 
      The web page will return the results of the ping command back to the user.  You will run a series of commands 
      to walkthrough the intended purpose of the web application.
      
      
**Payload One**

To test the webpage start by pinging the IP address:
`8.8.8.8`
and press submit to see the results display on the web application.

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Ping%208.8.8.8.png)

![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Results%20of%20Ping%20of%208.8.8.8.png)

  - Behind the scenes, when you select Submit, the IP you type in the field is injected into the command that is run against the Replicants webserver. The specific     command that ran on the webserver is `ping IP address` and `IP addresss: 8.8.8.8` is the `field value` that is injected into that command.   

**Payload Two**

Test Replicant webserver to see if it can be manipulated by inputing a different payload in the field by
`Typing: 8.8.8.8 && pwd`
   
![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/PWD%20Results.png) 
   
- The ping results above are the result of the second command used `pwd`.  The `injection` of `pwd` into the command line above is how you implement a:
  - Command Injection Attack

It should be noted that a Command Injection Attack is dependent on the web application taking user input to run a command against an operating system.

Now that you have determined that Replicants new application is vulnerable to command injection, you are tasked with using the dot-dot-slash method to design two payloads that will display the contents of the following files:

- /etc/passwd
- /etc/hosts
   
**Hint:** Test out commands directly on the command line in terminal to help design your payloads.

-  /etc/passwd
   - `Dot-Dot-Slash Payload One: 8.8.8.8 && cat ../../../../../etc/passwd`
![TODO:  Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Result%20for%20:etc:passwd.png)

-  /etc/hosts
   - `Dot-Dot-Slash Payload Two: 8.8.8.8 && cat ../../../../../etc/hosts`
![TODO: Update the path with name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/DVWA/Results%20for%20etc:hosts.png)

### Recommended mitigation strategies:

-  Strong input validation ie. whitelist certain commands like pwd and ls to only allow these input strings.
-  Restrict privilege to only the minimum needed to accomplish task which can in turn restrict a threat actor if they do        manage to inject commands.
-  Update and patch applications often.

## Web Application Two: Brute Force:

Complete the following steps to set up the activity:

### Step One:
  
Navigate to http://192.168.13.25

The page should look like the following:
![TODO: Update the path with name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/bWapp%20install.png)

Click `"here"` to install bWapp 🐝 at the bottom of the page.

Once the installation is a success, use the following credentials to login:

- Login credentials:

    * User Name: bee
    * Password:  bug
    * Set the security level: low

This will take you to the following page:
![TODO: Update the path with name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/bWapp%202nd%20page.png)

## Step Two

To access the application where we will perform our activity, enter in the following URL: 

http://192.168.13.35/ba_insecure_login_1.php

This will take you to the following page:
![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/bWapp%20broke%20auth.png)

-  This page is an administrative web application that serves as a simple login page. An administrator enters their username    and password and selects Login.

    * If the user/password combination is correct, it will return a successful message.
    * If the user/password combination is incorrect, it will return the message, "Invalid credentials."

We will use this page with another application called `Burp Suite` to complete this activity.
-  If not already installed run `sudo burpsuite` in Vagrant command line. Then open Firefox where the add-on `FoxyProxy` was installed prior to this activity.

      * Use the web application tool Burp Suite, specifically the Burp Suite Intruder feature, to determine if any of the           administrator accounts are vulnerable         to a brute force attack on this web application.

      * You've been provided with a list of administrators and the breached passwords below:
      * [List of Administrators](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/listofadmins.txt)
      * [List of Breached Passwords](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/breached_passwords.txt)

