# docker-symfony4
## What is included?
This is a docker compose configuration including a symfony 4 installation (website setup, not the smaller one), with nginx:1.17.0-alpine, mariadb:10.4.6 (build on ubuntu bionic), php:7.3.6-fpm (build on debian stretch), with an on the fly working configuration: That means start-up, visit localhost, that's it.

Nginx and mariadb are docker hub official images, php is slightly changed. Nginx config ist copy pasted from symfony manual.
## Setup - short description
### Step 1 for Mac OS
Install homebrew, if not already done:
```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Install git if not already done:
```bash
$ brew install git
```
Install docker desktop, if not already done:
```bash
$ brew cask install docker
```
Docker desktop includes docker-compose which is needed.
### Step 1 for other OS
On windows it is enough to install the windows docker desktop version you can download from [download.docker.com](https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe). Docker desktop includes the needed docker-compose.

On Linux you have to install docker first, which is well explained on [digitalocean.com howto](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04), and docker-compose separately which is described on [docs.docker.com](https://docs.docker.com/compose/install/).

Remember: To run this setup, docker and docker-compose is needed.

The docker-compose setup of this repository was never tested on other operating systems than Mac OS.
### Step 2 for any OS
To start your own project, you could just fork this repository into your git-hub account. But since you dont want your changes ever beeing integrated to my repository, or beeing related to my project as a github fork for ever, you should consider to duplicate it.

First, change to your local hard drives project directory, depending on the chosen approach, pick one of the following step 2.1.
#### 2.1 Fork and clone - not recommended -
Fork this repository to your git-hub account via the github web interface and clone your fork to your local harddrive:
```bash
$ git clone https://github.com/[your-github-user]/[your-fork-repo-name].git
```
#### 2.1 Mirroring this repository as your new project - recommended -
Create a bare clone of this repository:
```
$ git clone --bare https://github.com/StefanGerl/docker-symfony4.git
```
Mirror push it to your own, new repository:
```
$ cd docker-symfony4
$ git push --mirror https://github.com/[your-github-user]/[your-new-repository-name].git
```
Remove the temporary local repository you created before:
```
$ cd ..
$ rm -rf docker-symfony4
```
Checkout your own, new created duplicate of this repository to your local drive.
```
$ git clone https://github.com/[your-github-user]/[your-new-repository-name].git
```
This mirroring steps where taken from [github help](https://help.github.com/en/articles/duplicating-a-repository#mirroring-a-repository).
#### 2.2 Start the docker application container engine.
- Mac OS: Start Docker Desktop, if it's not auto started - Command + Space, type docker, hit enter.
- Windows: Start Docker Desktop, if it's not auto started - Startmenu, type docker, click Docker Desktop.
- Linux: Start the docker service, if it's not auto started. Depending on your linux version.
#### 2.3 Go to the directory and start the docker containers.
Go into the directory where you checked out your copy of this repository. Then run:
```bash
$ docker-compose up -d
```
#### 2.4 Run composer install inside the php machine
```bash
$ docker exec -it --user root docker-symfony4_php_1 bash
$ composer install
```
#### Open symfony start page
After that, open your browser and type http://localhost to the address field. If you can not see the symfony 4 start page, check [the known issues section](https://github.com/StefanGerl/docker-symfony4#known-issues) of this document.
#### Connect to DB
Choose a mariadb (most mysql clients should work) database client, for example on Mac OS: [Sequel Pro](https://www.sequelpro.com/), can easily be installed with:
```
$ brew cask install sequel-pro
```
Start client and add configuration, for sequel pro hit the plus-button on the bottom left. Use the following values for your new configuration (values in [] should be replaced with data of your choice):
- name: [Your favorite name]
- host: 127.0.0.1
- user: root
- password: root
- database: symfony

Stay with default values for the rest of the fields (port: 3306). Test and save the configuration, connect to database after. If you can not connect, check [the known issues section](https://github.com/StefanGerl/docker-symfony4#known-issues) of this document.

For sequel pro: Click on "test" button, the test has to be successfull, than click on "save". Click on "connect" button after, and now you are connected to the database server that will be used by the actual symfony 4 configuration.
## Pay attention
This setup and all credentials initialized with this docker setup are exposed on this repository in public. Be sure that you development environment is not reachable from outside your secured network, and change the whole configuration if you want to use this setup on staging or production (even if any attack should only harm you docker environment).
## Inspiration
The docker configuration is inspired by an [KNP Laps - Tutorial: How to dockerise a symfony 4 project](https://knplabs.com/en/blog/how-to-dockerise-a-symfony-4-project).
## Docker images
To change the docker images configurations, there are a lot of parameters that can be injected. You can find all possible parameters and values for the used docker images on their docker-hub pages, linked below.

The docker hub images that are used, are all official docker-hub versions, ubuntu and debian, alpine only for nginx.

I wanted to use "alpine only" in the beginning but: for the php container it was more complicated with the lack of real benefits, the same for mariadb.
+ mariadb: [docker hub project page](https://hub.docker.com/_/mariadb) - mariadb:10.4.6, that is running inside a container running with [Ubuntu 18.04 "Bionic Beaver"](https://wiki.ubuntuusers.de/Bionic_Beaver/).
+ nginx: [docker hub project page](https://hub.docker.com/_/nginx) - nginx:1.17.0-alpine. nginx:1.17.0 server that is running inside a container running [Alpine Linux](https://de.wikipedia.org/wiki/Alpine_Linux).
+ php-fpm: [docker hub project page](https://hub.docker.com/_/php) - php:7.3.6-fpm that is running inside a container running [Debian 9 "DebianStretch"](https://wiki.debian.org/DebianStretch).
## Known issues
### Existing and running local webserver and/or database server
If you have a local webserver running on port 80 and/or a local database server running on port 3306, they are blocking the ports for this docker configuration.

If so, you can change the bound port of this configuration and use that for calling your page address ex. http://localhost:8080, or you can shut down your local web- and or databse server, before starting the docker containers.

You can find the port configuration in the .env file in the root of this repository.
