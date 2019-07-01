# docker-symfony4
## Setup short
### Step 1: Ubuntu
Install docker, docker compose and git, if not already done.
```bash
apt-get install docker docker-compose git
```
### Step 1: Mac OS
Install homebrew, if not already done.
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Install docker, docker compose and git if not already done.
```bash
brew install docker docker-compose git
```
### Step 2: All OS
To start a new symfony 4 project, with a docker configured dev environment you could just fork this repository into your git-hub account. But if you dont want your changes ever beeing integrated to repository, you should consider to duplicate it.
#### 2.1 Fork and clone
Fork this repository to your git-hub account via the github web interface and clone your fork to your local harddrive.
```bash
git clone https://github.com/[your-github-user]/[your-fork-repo-name].git
```
#### 2.1 Or duplicate to your new project
Details on duplication approach: https://help.github.com/en/articles/duplicating-a-repository.
#### 2.2 Go to the directory and start the docker containers.
```bash
cd docker-symfony4
docker-compose up -d
```
#### Test
After that, open your browser and type http://localhost to the adress field. If you can not see the symfony 4 start page, check if you have a local webserver running on port 80 blocking the docker port binding on the default web page port.
If so, you can change the bound port and use that for calling your page address ex. http://localhost:8080, or shut down your local webserver.
#### Connect to DB
Choose a mariadb (most mysql clients should work) database client, for example https://www.sequelpro.com/ can be installed with:
```
brew cask install sequel-pro
```
Start client and add configuration, for sequel pro hit the plus-button on the bottom left. Use the following values for your new configuration (values in [] should be replaced with data of your choice):
- name: [Your favorite name]
- host: 127.0.0.1
- user: root
- password: root
- database: symfony

Stay with default values for the rest of the fields (port: 3306). Test and save the configuration, connect to database after. For sequel pro: Click on "test" button, the test has to be successfull, than click on "save". Click on "connect" button after, and now you are connected to the database server that will be used by the actual symfony 4 configuration from this installation.
## Pay attention
This setup and all credentials initialized with this docker setup are exposed on this repository in public. Be sure that you development environment is not reachable from outside your secured network, and change the whole configuration if you want to use this setup on staging or production (even if any attack should only harm you docker environment).

## Inspiration
The docker configuration is inspired by https://knplabs.com/en/blog/how-to-dockerise-a-symfony-4-project.

## Docker images
To change the docker images configurations, there are a lot of parameters that can be changed. You can find a configuration for those on their docker-hub pages. The docker hub images that are used, are all official docker-hub versions, ubuntu and debian, alpine only for nginx (I wanted to use alpine only in the beginning but: for php it was more complicated with the lack of real benefits, the same for mariadb):
+ mariadb: https://hub.docker.com/_/mariadb - mariadb:10.4.6, that is based on ubuntu bionic.
+ nginx: https://hub.docker.com/_/nginx - nginx:1.17.0-alpine.
+ php-fpm: https://hub.docker.com/_/php - php:7.3.6-fpm - that is based on debian stretch.
