# docker-symfony4
## What is this?
This is an easy way to start your own git versioned, github hosted, symfony 4 development environment, based on a docker-compose setup, including any step to install local prerequisites on Mac OS, as the perfect solution for working on a symfony 4 project as a team.

Installing the local prerequisites on Linux should be very similar changing this instructions from brew to the package manager that is delivered with your distribution, for Windows it is more complex. 

You can copy paste most of the commands, only commands related to your own github account have to be edited after pasting.

With that, mission can be accomplished in less than 6 minutes.
## What is included?
This is a docker compose configuration including a symfony 4 installation (website setup, not the smaller one), with nginx:1.17.0-alpine, mariadb:10.4.6 (build on ubuntu bionic), php:7.3.6-fpm (build on debian stretch).

Nginx and mariadb are docker hub official images, php is slightly changed. Nginx config ist copy pasted from symfony manual.
## Setup - short description
If you still have questions after reading the short description here, or you want to go deeper into it, or you want to start a discussion about this solution, there is a detailed description on my website: https://stefan-gerlinger.com/symfony-4-project-development-environment-in-less-than-6-minutes/.

I am happy with every input I get. 

### Step 1: Mac OS
Install homebrew, if not already done.
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Install docker, docker compose and git if not already done.
```bash
brew install docker docker-compose git
```
Install docker desktop
```bash
brew cask install docker
```
### Step 2: All OS
To start your own project, you could just fork this repository into your git-hub account. But since you dont want your changes ever beeing integrated to my repository, or beeing related to my project as a github fork for ever, you should consider to duplicate it.

On the other hand, the more often my repository is forked the more likely people will know it.
#### 2.1 Fork and clone - not recommended -
Fork this repository to your git-hub account via the github web interface and clone your fork to your local harddrive.
```bash
git clone https://github.com/[your-github-user]/[your-fork-repo-name].git
```
#### 2.1 Or duplicate it as your new project - recommended -
Follow these 4 easy steps: https://help.github.com/en/articles/duplicating-a-repository#mirroring-a-repository
#### 2.2 Start the docker environment
Mac OS: Command + Space, type docker, hit enter ;)
#### 2.3 Go to the directory and start the docker containers.
```bash
cd docker-symfony4
docker-compose up -d
```
#### 2.4 Run composer install inside the php machine
```bash
docker exec -it --user root docker-symfony4_php_1 bash
composer install
```
#### Test
After that, open your browser and type http://localhost to the address field. If you can not see the symfony 4 start page, check the known issues section of this document.
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

Stay with default values for the rest of the fields (port: 3306). Test and save the configuration, connect to database after.

For sequel pro: Click on "test" button, the test has to be successfull, than click on "save". Click on "connect" button after, and now you are connected to the database server that will be used by the actual symfony 4 configuration.
## Pay attention
This setup and all credentials initialized with this docker setup are exposed on this repository in public. Be sure that you development environment is not reachable from outside your secured network, and change the whole configuration if you want to use this setup on staging or production (even if any attack should only harm you docker environment).
## Inspiration
The docker configuration is inspired by https://knplabs.com/en/blog/how-to-dockerise-a-symfony-4-project.
## Docker images
To change the docker images configurations, there are a lot of parameters that can be injected, you can find all possible parameters and values for the used docker images on their docker-hub pages, linked below.

The docker hub images that are used, are all official docker-hub versions, ubuntu and debian, alpine only for nginx.

I wanted to use "alpine only" in the beginning but: for the php container it was more complicated with the lack of real benefits, the same for mariadb. You can start a discussion about that on the repositories detailed website. You can find a link in the project description.
+ mariadb: https://hub.docker.com/_/mariadb - mariadb:10.4.6, that is running inside a container running with ubuntu bionic.
+ nginx: https://hub.docker.com/_/nginx - nginx:1.17.0-alpine.
+ php-fpm: https://hub.docker.com/_/php - php:7.3.6-fpm that is running inside a container running debian stretch.
## Known issues
### Existing and running local webserver and/or database server
If you have a local webserver running on port 80 and/or a local database server running on port 3306, they are blocking the ports for this docker configuration.

If so, you can change the bound port of this configuration and use that for calling your page address ex. http://localhost:8080, or you can shut down your local web- and or databse server, before starting the docker containers.

You can find the port configuration in the .env file in the root of this repository.
