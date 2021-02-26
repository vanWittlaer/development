# Shopware 6 docker template

This is a docker setup to facilitate local plugin and theme development for Shopware 6.

It was derived from Shopware's https://github.com/shopware/development template.

To install a production Shopware 6 instance `git clone https://github.com/shopware/development shopware` and
follow the instructions therein. Alternatively, `mkdir shopware && cd shopware` and download the recent
Shopware 6 install zip-file and follow the standard Shopware 6 installation procedure.

# Setup Storefront Hot Watch

1. For your saleschannel define a domain as `http:localhost:9998`

1. Project root .env variables (note this file might be .gitignored)
```
APP_URL=http://localhost
STOREFRONT_PROXY_PORT=9998
ESLINT_DISABLE=true
```

2. vendor/shopware/storefront/Resources/views/storefront/base.html.twig

Line #2: `{% set isHMRMode = true %}`

3. SSH into app container `.psh.phar docker:ssh`

4. `cd shopware`

5. `bin/watch-storefront.sh`

# Create DB dump

Use a command like

`docker exec project_app_mysql_1 /usr/bin/mysqldump -uapp -papp shopware > local_201105_1642.sql`

to create the dump using the mysql app's mysqldump command. The mysqlcommand based on Mariadb currently in the app server may not output the dump properly (typical error when attempting to reload the dump: `The value specified for generated column 'reversed' in table 'product_keyword_dictionary' is not allowed.`).
