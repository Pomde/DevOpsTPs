# DevOpsTPs

## TP1 

### 1-1 Document your database container essentials: commands and Dockerfile.
See the comments in database/Dockerfile. To run the dockerfile, execute this command :
```docker run --name database -it -v /my/own/datadir:/var/lib/postgresql/data ./database```
- `--name` allows you to assign a name to the container
- `-it` allows you to run the docker in interactive mode to let you use the terminal even with the container running
- `-v /my/own/datadir:/var/lib/postgresql/data` allows you to specify a volume to use to persist data accross multiple runs of the container `/my/own/datadir` is the path to a local file and `/var/lib/postgresql/data` is the path to the file in the container

### 1-2 Why do we need a multistage build? And explain each step of this dockerfile.
We use a multistage build because we need to build the jar of the application first so we need java sdk and maven. 
But then, to run the docker, we only need the java jre, and the image with only java jre is smaller than the first one so we do that to get rid of useless things there could be in the first image and gain space.

### 1-3 Document docker-compose most important commands and 1-4 Document your docker-compose file.
For each container, create a service to run this container with build referencing the corresponding folders the Dockerfile. Also create a network to be able to communicate across the containers. Also added the volume that was already used in the first command, but this volume was created with docker instead of a bind mount.

### 1-5 Document your publication commands and published images in dockerhub.
- `docker tag my-database USERNAME/my-database:1.0`
- `docker push USERNAME/my-database`

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