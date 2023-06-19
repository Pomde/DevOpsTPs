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
  - This command allows you to create a tag referencing a docker image, in this case the my-database image 
- `docker push USERNAME/my-database`
  - This command allows you to upload an image to a registry, in this case dockerhub
  - To execute this command, make sure you have logged into your account with this command : `docker login`

## TP2 

### 2-1 What are testcontainers ?
Testcontainers is a library to create isolated environments to run tests. This is especially useful in our case because the environment is the same no matter the machine, the same way as docker, which is really useful as a developer to make sure tests are always made in the same environment. Also, like docker, they work fine in a CI context

### 2-2 Document your Github Actions configurations. 

### 2-3 Document your quality gate configuration.
We have created three workflows to be able to achieve an optimal CI. One workflow is in charge of the backend test, one workflow is in charge of building and pushing all images except the backend. Then one workflow is in charge of building and pushing the image of the backend. The workflows are separated this way to allow the first two workflows to run parallely and also run the last workflow for building the backend as soon as the tests are a success. If the tests fail, then we don't run this workflow

### Document your quality gate configuration.

## TD3

### Commandes utilisées 
- `ansible all -m ping --private-key=.ssh/id_rsa -u centos`
- `ansible all -m yum -a "name=httpd state=present" --private-key=.ssh/id_rsa -u centos --become`
- `ansible all -m shell -a 'echo "<html><h1>Hello World</h1></html>" >> /var/www/html/index.html' --private-key=.ssh/id_rsa -u centos --become`
- `ansible all -m service -a "name=httpd state=started" --private-key=.ssh/id_rsa -u centos --become`

## TP3

### 3-1 Document your inventory and base commands
To use your inventory, you can execute this command : `ansible all -i ansible/inventories/setup.yml -m ping`
- `-i ansible/inventories/setup.yml` to specify the inventory to use
- `-m ping` use the module ping
- `all` execute this command on all hosts in the inventory

### 3-2 Document your playbook
- To create a new role, execute this command : `ansible-galaxy init ansible/roles/docker`. All the roles files will be stored in the roles/docker folder
- We have created a role for each task to remove any task from the main playbook. There have been some issues concerning the python interpreter with a fix made in playbook.yml file.
- To use this playbook with our inventory, execute this command : `ansible-playbook -i ansible/inventories/setup.yml ansible/playbook.yml`

### 3-3 Document your docker_container tasks configuration.
All tasks have been documented in their specific documents. For each docker container, we remove it before starting it to make sure to use the latest version


For advanced documentation, please refer to each file as they are documented