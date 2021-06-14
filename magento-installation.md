# Magento 2.4.1 installation with Virtualmin

### Prerequisites

##### ssh to the root of your server (ssh root@123.456.78.90) and run those commands:

###### Add repository for necessary php packages
`sudo add-apt-repository ppa:ondrej/php`
###### Install all necessary php packages
`sudo apt install php7.4-common php7.4-gmp php7.4-curl php7.4-soap php7.4-bcmath php7.4-intl php7.4-mbstring php7.4-xmlrpc php7.4-mcrypt php7.4-mysql php7.4-gd php7.4-xml php7.4-cli php7.4-zip`
###### Magento 2.4.1 requires the elasticsearch follow this documentation to set it up
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-20-04



### Create New Virtual Server

##### Now go into the virtualmin, create a new virtual server, add dns records, add ssl wit Let's Encrypt. After that ssh into your new virtual server, cd to public_html and run
###### You need to clean up the contents of the public_html folder first
`rm -rf *`

`composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.1 ~/public_html`

It will ask you for your username and password, to get them go to https://marketplace.magento.com/ go to profile -> access keys and copy the credentials. public key is your username, private key is the password. Then composer will ask you if you want to store your credentials in the auth.json, you can say yes. then composer will download all dependencies. After its done run these two commands:

`find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;`
###
`find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;`

### 
`bin/magento setup:install --base-url=http://test.maroungrey.com/ --db-host=localhost --db-name=dbtest --db-user=test --db-password=password --admin-firstname=Maroun --admin-lastname=Magento --admin-email=myemail@gmail.com --admin-user=magentoadmin --admin-password=password --language=en_US --currency=USD --timezone=America/Chicago --use-rewrites=1`
### Sample data
`bin/magento sampledata:deploy`


