# Magento Commands
Quick commands lookup library for magento


* FULL CLEAN UP *

grunt clean && grunt exec && grunt less && grunt watch

php bin/magento setup:upgrade && php bin/magento cache:flush && php bin/magento cache:clean && php bin/magento setup:static-content:deploy -f && php bin/magento setup:di:compile


* RUN COMMAND AS SUDO *

ssh -t $USER@server006.web.com "sudo cat /etc/shadow"


* CLEAR THE COMPILED CODE AND CACHE *

php7.3 bin/magento setup:upgrade
php7.3 bin/magento cache:clean
php7.3 bin/magento cache:flush
php7.3 bin/magento setup:static-content:deploy -f
php7.3 bin/magento setup:di:compile


* ENABLE / DISABLE EXTENSION *

php bin/magento module:status       (view all modules)
php bin/magento module:disable <ExtensionProvider_ExtensionName> --clear-static-content
php bin/magento setup:upgrade        (update the DB)

cd app/code/<ExtensionProvider>/
rm -rf <ExtensionName>


* REMOVE CACHED FOLDERS *

!!! backup the pub/static/.htaccess !!!

rm -rf pub/static/* && rm -rf var/cache/* && rm -rf var/composer_home && rm -rf var/generation && rm -rf var/page_cache && rm -rf var/view_preprocessed


/*SWITCH MODE*/

bin/magento maintenance:enable
bin/magento maintenance:disable

bin/magento deploy:mode:show
bin/magento deploy:mode:set production
bin/magento deploy:mode:set default
bin/magento deploy:mode:set developer



* REGENERATE VENDOR *

/usr/bin/php7.3 /usr/local/bin/composer update


* REINDEX *

bin/magento indexer:info
bin/magento indexer:reindex


* SHITSHOW WITH URLS *

!!!TRUNKATE url_rewrites!!!
php bin/magento  cadence:urldedup:categories
php bin/magento  cadence:urldedup:products
php bin/magento ok:urlrewrites:regenerate
php bin/magento cache:clean
php bin/magento cache:flush
bin/magento indexer:reindex


* ELASTICSEARCH NO ALIVE NODES *

ssh to root user
sudo systemctl start elasticsearch
sudo systemctl status elasticsearch

/**/
xdebug.remote_enable=0
xdebug.remote_autostart=0  


UPDATE MAGENTO

composer require magento/product-community-edition=2.4.1 --no-update
composer update

find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;
find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;


