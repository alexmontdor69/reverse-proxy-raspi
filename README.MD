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

# How to
# Install the reverse-proxy
1. Download this repo in your raspi
`git clone ... `
2. Create a docker network
`sudo docker network create`
3. Add your self-signed ssl certs
Here i used the digital ocean approach.
`cd certs`
`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./nginx-selfsigned.key -out ./nginx-selfsigned.crt`
`cd ..`
`sudo openssl dhparam -out ./dhparam.pem 4096`

`sudo cp `


3. Create the local reverse-proxy
`sudo docker-compose up -d`

## Install a new application


a docker-compose.yml will have to be create following the template (**NAME OF THE TEMPLATE**)
the configuration file .env will have to be filled





## References
* Create a local DNS Server [https://github.com/tschaffter/docker-dnsmasq]
* Creating a Self-Signed SSL [https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-22-04]