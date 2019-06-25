# docker-symfony4
## Setup short
```bash
apt-get install docker docker-compose
git clone https://github.com/StefanGerl/docker-symfony4.git
cd docker-symfony4
docker-compose up -d
```
After that, open your browser and type http://localhost to the adress field. If you can not see the symfony 4 start page, check if you have a local webserver running on port 80 blocking the docker port binding on the default web page port.
If so, you can change the bound port and use that for calling your page address ex. http://localhost:8080, or shut down your local webserver.

## Pay attention
This setup and all credentials initialized with this docker setup are exposed on this repository in public. Be sure that you development environment is not reachable from outside your secured network, and change the whole configuration if you want to use this setup on staging or production (even if any attack should only harm you docker environment).
