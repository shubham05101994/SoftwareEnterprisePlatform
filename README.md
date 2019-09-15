
What is Ansible?
Ansible is an automation tool used for configuration management and application deployment/undeployment on various servers or machines at one go.
Admin sends one set of instructions on a machine and the same is passed to all the other connected hosts/servers.
                
•	Inventory File : This file contains the group of hosts upon which the commands and tasks from playbook operate.
•	Playbook : Playbook contains a set of instructions to be executed on the hosts/group mentioned in inventory file. Ansible uses YAML file for expressing Playbooks.

Purpose:

The main objective is to configure Ansible to deploy webserver, and bring it up a port 80 with a web page that is publicly accessible that displays the message: “Hello World” and to deploy and un-deploy the resources through Ansible playbook

Scope: This document provides details on
●	Creation of 2 virtual machines on AWS (Amazon Web Service) EC2 instance , one machine as Master and another machine as Stage.
●	Installation of Ansible on Master virtual machine
●	deploy.yml: Creation of a playbook to install Ngnix webserver, configure Ngnix to bring it up a port 80 and create and enable virtual hosts
●	undeploy.yml: Creation of a playbook file to disable and remove virtual hosts and uninstall the Ngnix webserver.
Basic Requirements:
●	A Linux, Ubuntu or Mac OS X computer 
●	AWS account
●	A code editor or IDE of your choice.
●	A terminal and ssh client for running Ansible against target hosts. 
Part-1: Create an HTML file to display the message “Hello World” on web page

 

Part-2: Create Virtual Machines on AWS through EC2
●	Login to https://console.aws.amazon.com
○	Click on “Services” and under “Compute” choose EC2.
○	Select the Instance type as “t2.micro” and click on “Review and launch” button.
○	Configure Instances details by providing a few of the basic details like:
Number of the instances to be created : 2
○	Configure Security Groups→ add ‘HTTP’ in Type tab
○	Create a key pair for the EC2 instance → the key generated for the EC2 instance is “bestone.pem”
○	Click on “Review and Launch” button
●	Now we have a running EC2 instance available with us.
●	Configure Elastic group:
○	On the left pane of the AWS portal, scroll down to “Network & Security”; Click on Elastic IP → Allocate New Address → Allocate.
○	With the new allocated IP, click on the “Actions” → Associate address → choose your EC2 instance. Thus, a permanent IP address gets assigned to the EC2 instance.
○	Make note of the Public DNS (IPV4) and the new elastic Public IP.
●	These instances contain both public and private ssh key that has to be used to do the handshake between systems within the network through Private IP of the systems.

Part-3: Install Ansible on virtual machines
●	Open Git-bash for Master Node and write the below code to install Ansible
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install python -y
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible

●	Once Ansible is installed successfully, write the code below for verification of successful installation and version
sudo ansible –m ping all


 
Part-4: Create an Inventory file having the list of all the hosts where the deployment has to be performed
 

Part-5: Create a Playbook file deploy.yml to:
●	Install Ngnix webserver on master machine
 
●	Configure Ngnix to bring it up a port 80: 
 

●	Run playbook deploy.yml. The file Executes and exits successfully.
		 
●	Enter the public ip / domain name of the EC2 instance or secondary droplet. Displays the “Hello World” message
Web Page URL: http://34.224.200.197/
Note: Currently the instances are stopped temporarily.






 
Part-6: Create a Playbook file undeploy.yml to:
●	Uninstall Ngnix server
●	Disable and remove virtual host
●	Clear cache


 
Reference:
https://docs.ansible.com/
https://docs.ansible.com/ansible/latest/installation_guide/intro_configuration.html
https://console.aws.amazon.com
https://docs.ansible.com/
https://www.ansible.com/resources/videos/quick-start-video
https://www.youtube.com/watch?v=xMHVvHZ-Zn4&t=1057s

Github Lin:  https://github.com/shubham05101994/SoftwareEnterprisePlatform.git
