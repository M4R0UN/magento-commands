# Magento installation for virtualmin
###### I will be installing magento 2.3.0 which compatible with php7.1 and 7.2
###### Before the installation make sure you have all necessary packages. Ssh to the root and run:
`sudo apt install php7.1 libapache2-mod-php7.1 php7.1-common php7.1-gmp php7.1-curl php7.1-soap php7.1-bcmath php7.1-intl php7.1-mbstring php7.1-xmlrpc php7.1-mcrypt php7.1-mysql php7.1-gd php7.1-xml php7.1-cli php7.1-zip`

### Create a new virtual server, create the ssl, create the dns record and change the php version to 7.1
### Ssh to your new server and check the php version. If php version in ssh is not 7.1 then ssh to the root and run:

`sudo update-alternatives --set php /usr/bin/php7.1`
cd to public_html and run:
`composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.3.0`
login in https://marketplace.magento.com/ go to profile -> access keys and copy the credentials. public key is your username, private key is the password. Then composer will ask you if you want to store your credentials in the auth.json, you can say yes. then composer will download all dependencies. After its done if you are using virtualmin you need to run these:
`find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;`
`find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;`
