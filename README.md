# Magento / Linux Commands lookup

### MOST USED
###### Search first 5 occurences
`grep -r '' | sed 5q`
###### Exception log
`tail -f var/log/exception.log`
###### Var clean folder:
`php bin/magento v:c`
###### Grunt:
`grunt clean && grunt exec && grunt less && grunt watch`
###### Maintenance:
`bin/magento maintenance:enable`
###### List of extentions:
`php bin/magento module:status`
###### Full cleanup:
`php bin/magento se:up && php bin/magento c:f && php bin/magento c:c && php bin/magento s:s:d -f && php bin/magento  s:d:c`


### CLEANUP

##### Update the DB:
`php bin/magento setup:upgrade`
##### Change URL of the static files and force browser to load the new version:
`php bin/magento setup:static-content:deploy -f`
##### Compile the code. Generate the contents of the *generated* folder:
`php bin/magento setup:di:compile`


### CACHE MANAGEMENT

##### Deleting all items from enabled Magento cache types only. Can clean specific types, e.g.: config, layout, block_html, collections, reflection, db_ddl, eav, etc.
`php bin/magento cache:clean`
##### Cleaning the cache in the website:
`php bin/magento cache:flush`
##### Enable cache:
`php bin/magento cache:enable`
##### Disable cache:
`php bin/magento cache:disable`
##### View status of cache:
`bin/magento cache:status`


### REMOVE CACHED FOLDERS

**!!! backup the pub/static/.htaccess !!!**

`rm -rf pub/static/* && rm -rf var/cache/* && rm -rf var/composer_home && rm -rf var/generation && rm -rf var/page_cache && rm -rf var/view_preprocessed`


### ENABLE / DISABLE EXTENSION

##### View all modules:
`php bin/magento module:status`
##### Disable module:
`php bin/magento module:disable <ExtensionProvider_ExtensionName> --clear-static-content`
##### Delete module:
`rm -rf app/code/<ExtensionProvider>/<ExtensionName>`


### MAINTENANCE

##### Enable:
`bin/magento maintenance:enable`
##### Disable maintenance:
`bin/magento maintenance:disable`


### CHANGE MODE

##### Show current mode:
`bin/magento deploy:mode:show`
##### Change mode:
###### Production
`bin/magento deploy:mode:set production`
###### Default
`bin/magento deploy:mode:set default`
###### Developer
`bin/magento deploy:mode:set developer`


### INDEXER

##### View list of indexers:
`bin/magento indexer:info`
##### View status of all indexers:
`bin/magento indexer:status [indexer]`
##### Reindex all indexers one time:
`bin/magento indexer:reindex`


### REGENERATE VENDOR FOLDER

`/usr/bin/php7.3 /usr/local/bin/composer update`


### RUN COMMAND AS SUDO

`ssh -t $USER@server006.web.com "sudo cat /etc/shadow"`


# Specific problems or tasks

### Magento 2.4.1 ReCaptcha disable [Invalid block type: MSP\ReCaptcha\Block\Frontend\ReCaptcha]
###### will disable recaptcha on the admin login
`bin/magento security:recaptcha:disable-for-user-login`



### URL REWRITE

**!!!TRUNKATE url_rewrites!!!**
###### Install Cadence
`mkdir -p app/code/Cadence/UrlDedup && git clone https://github.com/cadencelabs/urldedup app/code/Cadence/UrlDedup`

`php bin/magento setup:upgrade`

`php bin/magento  cadence:urldedup:categories`

`php bin/magento  cadence:urldedup:products`

###### Regenerate URL

`php bin/magento ok:urlrewrites:regenerate`

###### Flush the Cache

`php bin/magento cache:clean`
`php bin/magento cache:flush`

###### Reindex

`bin/magento indexer:reindex`


### ELASTICSEARCH NO ALIVE NODES

ssh to root user

`sudo systemctl start elasticsearch`
`sudo systemctl status elasticsearch`

### UPDATE MAGENTO 

`composer require magento/product-community-edition=2.4.1 --no-update`
`composer update`

### Virtualmin specific config for .htaccess (use after updating magento)

`find . -name .htaccess -exec sed -i 's/FollowSymLinks/SymLinksIfOwnerMatch/g' {} \;`
`find . -name .htaccess -exec sed -i 's/Options All -Indexes/Options -Indexes/g' {} \;`


