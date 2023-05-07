---
title: 'Run a docker registry in a LXC Environment with SSL and Login'
date: 2019-12-12
categories: [IT]
tags: [debian, ssl, docker, registry, lxd, lcx, linux]
---


##### LXD/LXC  

Fire up an Debian 10 in a LXC Container and name it "docker-registry  
lxc launch images:debian/10 docker-registry

Adjust the behavior of the LXC Container, otherwise docker wont't be able to work  
<pre>lxc config set docker-registry security.nesting true</pre>  
<pre>lxc config set docker-registry security.privileged true</pre>  
  cat <<EOT | lxc config set docker-registry raw.lxc -  
  lxc.cgroup.devices.allow = a  
  lxc.cap.drop =  
  EOT  
  
##### Enter the LXC Container
<pre>lxc exec docker-registry -- /bin/bash</pre>  


##### Install Software prerequisites
<pre>apt install apt-transport-https ca-certificates curl software-properties-common gnupg2</pre>  

##### Add the Repository
URL: https://download.docker.com/linux/debian/dists/buster/stable/  
<pre>curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -</pre>  

##### Read new Repository  
<pre>apt-get update</pre>  

##### Verfiy that only this Repository is used for Docker Updates and install  
<pre>apt-cache policy docker-ce</pre>   

##### Install docker-ce  
<pre>apt install docker-ce -y</pre>  

##### Check that the Docker Service is up and running  
<pre>systemctl status docker</pre>  

##### Install the latest Docker Compose from docker git 
URL: https://github.com/docker/compose/releases   
<pre>curl -L https://github.com/docker/compose/releases/download/1.25.1-rc1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose</pre>  

##### Make it executable
<pre>chmod +x /usr/local/bin/docker-compose</pre> 

##### setup environment
<pre>mkdir -p /opt/{registry_certs,docker_reg_auth,datafiles}  
cd /opt</pre>  

##### create the htpasswd user and password file
<pre>docker run -it --entrypoint htpasswd -v $PWD/docker_reg_auth:/auth -w /auth registry:2 -Bbc /auth/htpasswd admin admin</pre>  

##### adjust the openssl.cnf
###### copy the original one
<pre>cp /etc/ssl/openssl.cnf /etc/ssl/openssl.cnf.backup</pre>  

<pre>
-----edits------
at the beginning

####################################################################
.
.
[ req ]
default_bits            = 2048
default_keyfile         = privkey.pem
distinguished_name      = req_distinguished_name
attributes              = req_attributes
x509_extensions = v3_ca # The extensions to add to the self signed cert  <---------comment out
.
.
.
.
.
[ v3_req ]

# Extensions to add to a certificate request

basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment

[ v3_ca ]

# IP: Addresses or DNS: for each host needed
subjectAltName = IP:192.168.1.2,IP:192.168.1.4

# Extensions for a typical CA
-----edits-end-------
</pre>

##### create the ssl certificates
######on the host, that is running the docker registry
###### still in the /opt directory
<pre>openssl req -newkey rsa:4096 -nodes -sha256 -keyout registry_certs/domain.key -x509 -days 3560 -out registry_certs/domain.cert</pre>

##### on the remote host (notebook, workstation, client)
<pre>sudo mkdir -p /etc/docker/certs.d/192.168.1.2:5000  
sudo scp -i /home/tux/.ssh/id_rsa root@192.168.1.2:/opt/registry_certs/domain.cert /etc/docker/certs.d/192.168.1.2:5000/ca.crt</pre>  

##### run the docker in foreground registry
<pre>docker run -p 5000:5000 -v $(pwd)/registry_certs:/certs -v $(pwd)/docker_reg_auth:/auth -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.cert -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -e REGISTRY_AUTH=htpasswd --restart=always --name registry registry:2</pre>  

##### Docker Compose File
<pre>
version: '3'

services:
  registry:
    restart: always
    image: registry:2
    ports:
    - "5000:5000"
    environment:
      REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /datafiles
      REGISTRY_HTTP_TLS_CERTIFICATE: /certs/domain.cert
      REGISTRY_HTTP_TLS_KEY: /certs/domain.key 
      REGISTRY_AUTH_HTPASSWD_REALM: "Registry Realm" 
      REGISTRY_AUTH_HTPASSWD_PATH: /auth/htpasswd
      REGISTRY_AUTH: htpasswd
    volumes:
      - ./docker_reg_auth:/auth
      - ./datafiles:/datafiles
      - ./registry_certs:/certs
</pre>  

###### You can start your registry as a background process, which will allow you to exit the ssh session and persist the process
<pre>docker-compose up -d</pre>  

##### login
<pre>docker login https://192.168.1.2:5000</pre>