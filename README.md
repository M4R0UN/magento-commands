# Magento Commands lookup

###### MostUsed

`grunt clean && grunt exec && grunt less && grunt watch
 
 bin/magento maintenance:enable
 
 php bin/magento module:status
 
 php bin/magento setup:upgrade && php bin/magento cache:flush && php bin/magento cache:clean && php bin/magento setup:static-content:deploy -f && php bin/magento  setup:di:compile`

###### Cleanup

Update the DB:
`php bin/magento setup:upgrade`
Change URL of the static files and force browser to load the new version:
`php bin/magento setup:static-content:deploy -f`
Generate the contents of the *generated* folder:
`php bin/magento setup:di:compile`


###### Clear Cache

Deleting all items from enabled Magento cache types only. Can clean specific types, e.g.: config, layout, block_html, collections, reflection, db_ddl, eav, etc.
`php bin/magento cache:clean`
Cleaning the cache in the website:
`php bin/magento cache:flush`
Enable/Disable cache:
`php bin/magento cache:enable
 php bin/magento cache:disable`


###### REMOVE CACHED FOLDERS

**!!! backup the pub/static/.htaccess !!!**

`rm -rf pub/static/* && rm -rf var/cache/* && rm -rf var/composer_home && rm -rf var/generation && rm -rf var/page_cache && rm -rf var/view_preprocessed`


###### ENABLE / DISABLE EXTENSION

View all modules:
`php bin/magento module:status`
Disable module:
`php bin/magento module:disable <ExtensionProvider_ExtensionName> --clear-static-content`
Delete module:
`rm -rf app/code/<ExtensionProvider>/<ExtensionName>`


###### SWITCH MODE

Enable / Disable maintenance
`bin/magento maintenance:enable
 bin/magento maintenance:disable`


###### CHANGE MODE

Show current mode:
`bin/magento deploy:mode:show`
Change mode:
`bin/magento deploy:mode:set production
 bin/magento deploy:mode:set default
 bin/magento deploy:mode:set developer`


###### INDEXER

View list of indexers:
`bin/magento indexer:info`
View status of all indexers:
`bin/magento indexer:status [indexer]`
Reindex all indexers one time:
`bin/magento indexer:reindex`


###### REGENERATE VENDOR FOLDER

`/usr/bin/php7.3 /usr/local/bin/composer update`


###### RUN COMMAND AS SUDO

`ssh -t $USER@server006.web.com "sudo cat /etc/shadow"`


# Specific problems

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


* UPDATE MAGENTO *

composer require magento/product-community-edition=2.4.1 --no-update
composer update

find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;
find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;


