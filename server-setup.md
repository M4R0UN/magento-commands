# Ubuntu 20.04 setup with digital ocean and virtualmin / webmin

### Create the droplet in digital ocean
###### I prefer 4gb of ram since I had some memory issues installing magento on 2gb. Wordpress was fine though
##### The hostname have to be the domain with the subdomain
###### Example:
`gcp.maroungrey.com`
###### Have to consider the subdomain compatibility with cloudflare, so far I only had success with gcp, dev or test subdomains for some reason

### Ssh to the droplet and add user
##### After the droplet is created, grab the ipv4 in the top left corner and ssh to the root
###### Example:
`ssh root@123.456.78.90`
##### Then add the user
###### Example:
`adduser maroun`
##### Add sudo rights to a user
###### Example:
`usermod -aG sudo maroun`
##### Now you can exit the root
`exit`

### Check if the hostname setted up correctly
##### Now you can ssh to your user by only executing:
`ssh root@123.456.78.90`
##### Check if the hostname is correct and edit it if its wrong
`sudo nano /etc/hostname`
###### Here you should see your hostname, not the FQDN, for example if you see `gcp.maroungrey.com` change it to `gcp`
##### Next, you want to check if /etc/hosts file is right:
`sudo nano /etc/hosts`
###### Here you should see something like:
`127.0.1.1   gcp.maroungrey.com gcp`
######
`127.0.0.1   localhost`
###### If you had to edit anything, run:
`sudo reboot`

### Next install virtualmin
##### Get the package and install it:

`wget http://software.virtualmin.com/gpl/scripts/install.sh`
######
`sudo /bin/sh install.sh`

### DNS setup
##### Next step is setting up the DNS record in cloudflare
###### Add site and go to DNS tab. Now you need to set up few records.
###### Here is the example of configs that you need:

| Type | Name | Content | TTL | Proxy status |
| --- | --- | --- | --- | --- |
| A | maroungrey.com | 123.456.78.90 | Auto | DNS only |
| CNAME | gcp | maroungrey.com | Auto | DNS only |
| CNAME | www | maroungrey.com | Auto | DNS only |
| CNAME | www.gcp | maroungrey.com | Auto | DNS only |
| TXT | nxdomain | _acme-challenge.www.gcp.maroungrey.com | Auto | DNS only |

### Virtualmin
###### After you created the dns records you should be able to access the virtualmin by this url:
`https://gcp.maroungrey.com:10000/`
###### or ip:
`https://123.456.78.90:10000/`
###### Now virtualmin will walk you through the post installation configs. After you finish that you need to create ssl certificate in:
`Virtualmin -> Server Configuration -> SSL Certificate -> Let's Encrypt`
###### After that you need to enable the SSL Certificate in Webmin:
`Webmin -> Webmin -> Webmin Configuration -> SSL Encryption`
###### Enable the SSL and create a new SSL certificate in Let's Encrypt


# Installing MySQL and phpmyadmin
###### Test if you are able to log in into mysql. If you are then proceed to Install phpmyadmin step. If you cant, read below.
`sudo mysql`
##### or 
`mysql -u root -p`
##### Exit
`exit`
### Configuring/Installing My SQL
##### Virtualmin installs mysql automatically but I sometimes bump into the autorization error when trying to setup MySQL, so I just reinstall it and start from scratch. If you experiencing the same follow those steps:
##### Uninstall mysql (from the root)
`sudo apt-get remove --purge mysql*`
`sudo apt-get autoremove`
`sudo apt-get autoclean`
###### Install mysql
`sudo apt install mysql-server`
###### This script will remove some insecure default settings and lock down access to your database system. Firstly it will ask you to enable VALIDATE PASSWORD COMPONENT. Choose No for that one, set the password and proceed through the other settings as you like, I usually just put no for everything.
`sudo mysql_secure_installation`
###### Test again if you are able to log in into mysql
`sudo mysql`
### Install phpmyadmin
###### Follow this documentation
`https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04`
###### If after that you see the php script instead of the phpmyadmin page, run following commands:
`$ sudo apt purge libapache2-mod-php7.4 libapache2-mod-php
$ sudo apt-get install libapache2-mod-php7.4
$ sudo a2enmod php7.4
$ sudo service apache2 stop
$ sudo service apache2 start`


# After steps
##### Now you can create a virtual server
`Virtualmin -> Create New Virtual Server`
###### Fill out the domain name and password, add necessary DNS records in cloudflare and create ssl with Let's Encrypt. After that you can install CMS and start developing your website. 


### Additional settings
##### Now the setup is pretty much good to go, you can set up the backups now and if you need to install different php version here are the steps:
###### Ssh to the root:
`ssh root@123.456.78.90`

https://tecadmin.net/install-php-ubuntu-20-04/

###### Now you can choose different php version in:
`Virtualmin -> Server Configuration -> PHP Options -> Versions`


