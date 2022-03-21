## Vulnerabilities-and-Hardening
(Cybersecurity Bootcamp Unit 15 Assignment)

# Topics Covered in this repository:
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

# Content will include steps on how to test the vulnerabilities of a web application using a virtual machine.  
Steps will include:  

- Detailing how to setup and access the applications
- A walkthrough of how the application is intended to work
- Task that will test the application for vulnerabilities

# To launch the environment with several vulnerable web applications, complete the following:

Use the command line to run Vagrant with the following command: 
- vagrant up

# Then, open terminal inside Vagrant and run the following on the command line: 
- cd ./Documents/web-vulns && docker-compose up

While the output might look like the task is still running, this script has launched several vulnerable web applications that we will use throughout this assignment.  Leave this page open and running then open a another terminal window.

http://192.168.13.25
Login credentials:

- User Name: admin
- Password:  password

(Note if your DVWA does not open to the menu screen scroll to the bottom and click create a database and login again.)

Select ## Command Injection option.






