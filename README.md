# DevOpsTPs

## TP1 

### 1-1 Document your database container essentials: commands and Dockerfile.

### 1-2 Why do we need a multistage build? And explain each step of this dockerfile.

### 1-3 Document docker-compose most important commands. 1-4 Document your docker-compose file.

### 1-5 Document your publication commands and published images in dockerhub.


## TP2 

### 2-1 What are testcontainers ?

### 2-2 Document your Github Actions configurations. 

### Document your quality gate configuration.

## TD3

### Commandes utilisées 
- ansible all -m ping --private-key=.ssh/id_rsa -u centos
- ansible all -m yum -a "name=httpd state=present" --private-key=.ssh/id_rsa -u centos --become
- ansible all -m shell -a 'echo "<html><h1>Hello World</h1></html>" >> /var/www/html/index.html' --private-key=.ssh/id_rsa -u centos --become
- ansible all -m service -a "name=httpd state=started" --private-key=.ssh/id_rsa -u centos --become

## TP3

### 3-1 Document your inventory and base commands

### 3-2 Document your playbook

### Document your docker_container tasks configuration.