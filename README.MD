# Create a reverse-proxy container system for Raspberry
# Objectives
Transform my Raspberry into a reverse-proxy to serve application in my local network



# Prerequisite
## Material
* Raspberry (tested with 3b+)
* SSD Drive (and not a Card)
## Software
* Raspbian version 11 bullseye ("Debian GNU/Linux 11 (bullseye)")
* Git
* Docker Engine - Community 20.10.17 / 1.41
* local DNS Server [https://thekelleys.org.uk/gitweb/?p=dnsmasq.git;a=summary]

# How the system works
A DNS server install on your LAN will manage local addresses (e.g my.project.local) and point these request to a reverse proxy. the reverse proxy will direct to application server corresponding to the client request.

The system will be a docker network that will include:
* a container for the reverse-proxy
* a container for each application
* a container for an installation helper

The proposed configuration will always use ssl and will be set up as such.

# How to ...
# Install the reverse-proxy
1. Download this repo in your raspi

`git clone ... `

2. Create a docker network

`sudo docker network create`

3. Add your self-signed ssl certs

Here i used the digital ocean approach.

```
cd certs
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./nginx-selfsigned.key -out ./nginx-selfsigned.crt
cd ..
sudo openssl dhparam -out ./dhparam.pem 4096

sudo cp
```


3. Create the local reverse-proxy

`sudo docker-compose up -d`

## Install a new application


a docker-compose.yml will have to be create following the template (**NAME OF THE TEMPLATE**)
the configuration file .env will have to be filled


## Read the different configuration files
### Application docker-compose.yml

### env.conf
_List of parameters used:_

VIRTUAL_HOST: is the name of the domain 
VIRTUAL_PORT: is the port on which the app is communicating
VIRTUAL_APP_PORT: is the unique port on which the app is communicating externally - only allowed by the localhost

`docker compose --env-file env.conf up -d`

### nginx.tmpl
The container nginx-gen is create a file to configure the nginx server. It is  located in /etc/nginx/conf.d/default.conf
Basically for each published container, nginx-gen will create a:
* upstream section
* server 80 section to redirect to 443
* server 443 section to redirect to a published container

# To-do
- [ ] correct Issues on reloading nginx
- [50%] Test Jeedom and external port
- [ ] Save the db external environment (google drive ?)

# References
* Create a local DNS Server [https://github.com/tschaffter/docker-dnsmasq]
* Creating a Self-Signed SSL [https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-22-04]
* Docker-gen github [https://github.com/nginx-proxy/docker-gen]
