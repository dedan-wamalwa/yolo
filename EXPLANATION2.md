# Deploying in a remote server
This document will take you through the steps to deploy this application on a remote server

## 1. Vagrantfile
 Here's the [Vagrantfile](/Vagrantfile).
 Inside the vagrantfile, I configured the ubuntu20.04 server and exposed port 3000 and 5000 of the VM to the host's similar ports. These ports run the client and backend microservices respectively
 I also disabled ssh key requirement
 I finally configured it to run an ansible playbook when the VM is provisioned

## 2. Ansible configuration files (ansible.cfg and hosts)
 Here are the files: [Ansible](/ansible.cfg) && [hosts](/hosts)
 ### Ansible.cfg
  In this file, I defined the inventory file, which is the hosts file, remote user, private key file and set host key checking to false to make the process easy. This setting can however be set to true to add a layer of security.
### hosts
 This is the inventory file that defines our server. It's the inventory that ansible wil use when the playbook is invoked. I defined the ansible host IP and port.

## 3. Roles
 Here's the [roles](/roles/) folder
 This folder contains the four roles that will be executed in the playbook:

 ### 1. update packages
  This role updates the package manager index in the VM
  Here's a link to the [role](/roles/update_packages/) folder.
 ### 2. install docker
  This role installs docker and docker-compose
  It has five tasks: Installing dependancies, Add docker GPG key, Add docker repository, Install docker engine and finally install docker-compose
  Here's link to the [role](/roles/install_docker/) 
 ### 3. clone github repository
  This role clones the github repository into the VM using git.
  It makes use of the vars key where our variables that hold the url to the repository and path to clone the repo are defined
  Here's a link to the [role](/roles/clone_repo/)
 ### 4. run docker-compose
  This role uses docker-compose to spin up the docker containers
  We start change directory using chdir= /.. to go to the directory where the repo was clone and then run the command docker-compose up -d to spin the containers in detach mode
  Here's a link to the [role](/roles/run-docker-compose/)

## 4. playbook
 This is the ansible playbook that executes tasks and roles and is executed when vagrant provisions the server
 At the beginning, we specify all hosts, but only one server will be used since only one is defined and become yes to become the super user in the server.
 In the playbook we run two pre_tasks: update packages and installing docker. This is the initial set up to deploy our app in the server. We then run the main tasks of cloning the repo and spining up containers using docker-compose.
 Note the use of include_role key to run the tasks in the roles defined earlier.



# SET UP
 - Create a directory in your local machine
 - Clone this repo in that directory
 - Change directory to this repo's name (i.e. yolo)
 - Run ```vagrant up```
 

