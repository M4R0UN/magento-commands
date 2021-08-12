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

# DNS setup
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

# Virtualmin Configurations
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
###### Test if you are able to log in into mysql. You need to enter the password that you specified in virtualmin post installation configs for mySQL.
`mysql -u root -p`
##### Configure the root account to authenticate with a password
`ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';`
##### Create a new db user
`CREATE USER 'maroun'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';`
##### Grant all priveleges to the new user
`GRANT ALL PRIVILEGES ON *.* TO 'maroun'@'localhost' WITH GRANT OPTION;`
##### Exit
`exit`

### Install phpmyadmin
###### Follow this documentation
https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04
###### If after that you see the php script instead of the phpmyadmin page, run following commands:
`$ sudo apt-get install libapache2-mod-php7.4`
`$ sudo a2enmod php7.4`
`$ sudo service apache2 restart`


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


