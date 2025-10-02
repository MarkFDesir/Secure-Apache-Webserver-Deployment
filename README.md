# Secure Apache Webserver Deployment


### Overview
In this project I deployed a secure Apache web server in a Docker container on an Ubuntu server to build skills in server setup, networking, and web development. The container used a bridged network and was configured to serve HTTPS traffic with a self-signed SSL certificate for local testing purposes until I registered my own domain for my website to be accessible on the web. I adjusted Apache settings, enabled key modules, and added HTTP security headers to harden the server. pfSense firewall rules were configured to allow proper traffic flow after resolving initial outbound blocking issues. The website, built with HTML, CSS, and JavaScript in VS Code, was deployed using docker. This project improved my hands-on experience with Docker, Apache web server, pfSense firewalls, and secure web deployment. If you want to learn more check out the projects page on my website.

## Docker Container Configuration

- The continer for my website is on a bridged network that I created so that the container could have its own IP own my network. This is known as IPVLAN L3 mode

Command to create docker network on Ubuntu Linux
```
sudo docker network create -d ipvlan \
> -o parent=networkInterface -o ipvlan_mode=l3 \
> --subnet networkSubnet \
> UbuntuServers

```
- I entered my own input for the networkSubnet and networkInterface placeholders respectively <br>

Command to run docker container on Ubuntu Linux
```
sudo docker run -itd   --name containerName   -p 80:80   -p 443:443   --network networkName   --ip ipAddress httpd:latest
```
- I entered my own input for the containerName, networkName, and ipAddress placeholders respectively <br>

## Apache Web Server Configuration
- Modified configuration files to allow  secure traffic through HTTPS  
- Defined the ServerRoot, DocumentRoot, and setting both ServerAdmin and ServerName to resolve hostname warnings. 
- Enabled several required modules for ssl, http headers, and socache shmcb. 
- To enable secure communications I generated a self-signed SSL certificate for testing purposes.
![CRT Generation](/Images/Crt_KeyGeneration.png "CRT Generation")
- Created a VirtualHost block with redirect permanent to my webserver's IP through HTTPS
- Hardened the Apache server by Disabled weak SSL protocols(SSLProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1)
- Set strong ciphers and cipher ordering
- Added security headers
![CRT Generation](/Images/virtualhost.png "CRT Generation")

## Static Site Development
- Developed static site using HTML,CSS, and JavaScript, chose not to use any frameworks to learn more fundementals of web development
- Used Visual Studio Code for development
- Tried multiple desgins for better UX
![Website Development Photo 1](/Images/devphoto1.png "Website Development Photo 1")
![Website Development Photo 2](/Images/devphoto2.png "Website Development Photo 2")
