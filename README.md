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
```bash
git clone https://github.com/StefanGerl/docker-symfony4.git
cd docker-symfony4
docker-compose up -d
```
After that, open your browser and type http://localhost to the adress field. If you can not see the symfony 4 start page, check if you have a local webserver running on port 80 blocking the docker port binding on the default web page port.
If so, you can change the bound port and use that for calling your page address ex. http://localhost:8080, or shut down your local webserver.

## Pay attention
This setup and all credentials initialized with this docker setup are exposed on this repository in public. Be sure that you development environment is not reachable from outside your secured network, and change the whole configuration if you want to use this setup on staging or production (even if any attack should only harm you docker environment).

## Inspiration
The docker configuration is inspired by https://knplabs.com/en/blog/how-to-dockerise-a-symfony-4-project.

## Docker images
To change the docker images configurations, there are a lot of parameters that can be changed. You can find a configuration for those on their docker-hub pages. The docker hub images that are used, are all official docker-hub versions, ubuntu and debian, alpine only for nginx (I wanted to use alpine only in the beginning but: for php it was more complicated with the lack of real benefits, the same for mariadb):
+ mariadb: https://hub.docker.com/_/mariadb - mariadb:10.4.6, that is based on ubuntu bionic.
+ nginx: https://hub.docker.com/_/nginx - nginx:1.17.0-alpine.
+ php-fpm: https://hub.docker.com/_/php - php:7.3.6-fpm - that is based on debian stretch.
