### Configuration management tool:
Possibilites
* through manual 
    - not an option
* shell scripting
    - difficult to understand
    - not an user friendly
* Scripting
    - easy to readble
    - easy understand
    - idempotence
* Tools that are using for scripting language
    - Ansible
    - chef  
* In configuration management tools we have two type of method
1. push
   * here master is communicate to the node to done the work
   * agentless
   example: Ansible
2. pull
    * here the nodes are used to communicate with the master at a pirticular intervel of time
    * agent is required
    example: chef

### Push and Pull configuration management
 ![Preview](.\ansible2.png)
* Basic things need to run the java or Dotnet applications
-----
java application
* server 
* tomact 
* stop/start the tomcat application

dot net appplication
* server
* IIS serrvice management
------

### Ansible
Ansible is a push type configuration management tool
it will assigne the work to the nodes
* Architecture of the Ansible
![Preview](.\ansible1.png)

### Ansible User Configuration
* In this series, lets create a user called as admin.
* If your vm is in AWS or any other virtualization provider with only key based authentication, we need to enable password based authentication.
* need to login into the server for that copy the ssh command to connect to the server and then update the server

   -----
   sudo apt-get update
   -----

* become root user
   -----
   sudo -i
   -----
* adding user
-----
adduser devops
-----
* user required sudo previlages for accessing root services
* for providing sudo previlages for user 
* we should edit the /etc/sudoers file and add the line 
* commend for opening the file sudoers file
-----
visudo
------
* add line under sudo group
-----
devops  ALL=(ALL:ALL) NOPASSWD:ALL
-----
enable the user login in server as password based authantication
* for this we should edit the sshd_configuration file 
* it is located in /etc/ssh/sshd_config
* and then edit the sshd_cofig file  
-----
vi /etc/ssh/sshd_config
password authantication no ---> enable to yes
-----
* we should restart the ssh service
-----
sudo service ssh restart
-----
* the above steps are repeat in node server
### installing ansible on Master node
* install the ansible software by using package manager 
* here we are using apt-get package manager
* updating the repository and installing the software
----- 
sudo apt-get update
sudo apt-get install ansible -y
-----
* for checking the version of ansible 
-----
ansible --version
-----
* installing python on worker node
----
sudo apt-get install python -y
----
### making connection to communicate between master node and slave node
* in master node we have generate the public and private keys 
-----
ssh-keygen
-----
* we have to copy the public key to the slave or worker node 
-----
ssh-copy-id \<username>@\<ip address>

ssh-copy-id devops@\<ip address>
-----
### Checking the connection
* on master node execute the command 
-----
ansible -i \<ip of slave> -m ping all
-----
* if the ping pong got success then the connection between the two nodes happends successfuly 
* now to make sure the connection happends between master and slave node, login to the slave node from the master node 


