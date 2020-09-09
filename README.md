# Ansible-assignment

### In this reposatory i Wrote an ansible playbook that do the following setup on remote Linux server:

* Connect to the server with username/password.
* Setup Tomcat
* Change Tomcat port to 9095
* Deploy a Single HTML file
* Start the service
* Stop the service

## steps:
* I create ubuntu ec2 instantce on AWS to act as Linux server.
* create a user with password in EC2 instance:
     1) Add a new user in EC2 using command:
    
       - sudo useradd username
           
     2) enable password authentication first before setting a user password:
     
       - Edit the sshd configuration file /etc/ssh/sshd_config as root.
       - Find the parameter PasswordAuthentication. Make sure it's uncommented and set to yes.
       - Save the file and exit. Restart ssh service for this to take effect.
       
     3) set the user password using command:
     
       - passwd username
           
     4) allow new user to have sudo privilage:
     
       - usermod -aG sudo username
       
    ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/1.png)

* I run anible-playbook on this server using command:

      - ansible-playbook -i inventory playbook.yml --ask-pass --extra-vars "ansible_sudo_pass=yourPassword"
      
    Note: i write username in inventory file
    
   ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/2.png)
   
   ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/3.png)
   
   To make sure that the port is replace successfully got to server.xml:
   
       - cat /opt/tomcat/conf/server.xml
    
   ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/5.png)
   
   to access tomcat from browser before deploying static html file : 3.19.31.174:9095
   
   ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/4.png)
   
      

* To Deploy a Single HTML file on tomcat:

     1- I opend server.xml file:
      
       - sudo vim /opt/tomcat/conf/server.xml
       
     2- Add  Context element inside the Host element:
     
        - <Context docBase="/home" path="/" />
        
    Note: docBase is the directory on disk that contains my static file and path is the URL that i want to serve the files on.
    

  ![alt text](https://github.com/shimaa829/Ansible-assignment/blob/master/ansible-screenshots/7.png)
  
  
 * The URL to access static html page:
   http://3.19.31.174:9095
