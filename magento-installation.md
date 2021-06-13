# Magento 2.4.1 installation for virtualmin

##### ssh to the root of your server and run those commands:

`apt get composer`
`sudo add-apt-repository ppa:ondrej/php`
`sudo apt install php7.4-common php7.4-gmp php7.4-curl php7.4-soap php7.4-bcmath php7.4-intl php7.4-mbstring php7.4-xmlrpc php7.4-mcrypt php7.4-mysql php7.4-gd php7.4-xml php7.4-cli php7.4-zip`




##### After that go into the virtualmin, create a new virtual server, add dns records, add ssl wit Let's Encrypt. After that ssh into your new virtual server and run
`composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.1`

It will ask you for your username and password, to get them go to https://marketplace.magento.com/ go to profile -> access keys and copy the credentials. public key is your username, private key is the password. Then composer will ask you if you want to store your credentials in the auth.json, you can say yes. then composer will download all dependencies. After its done run these two commands:

`find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;`
###
`find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;`


