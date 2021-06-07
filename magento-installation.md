# Magento installation for virtualmin
### I will be installing magento 2.3.0
### Create a new virtual server, create the ssl, create the dns record and change the php version to 7.1
### Ssh to your new server and check the php version. If php version in ssh is not 7.1 then ssh to the root and run:
`sudo update-alternatives --set php /usr/bin/php7.1`
cd to public html and run:
`composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.3.0`
login in https://marketplace.magento.com/ go to profile -> access keys and copy the credentials
