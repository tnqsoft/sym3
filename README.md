sym3
====

A Symfony project created on September 8, 2016, 2:31 pm.

```
<VirtualHost *:80>
    ServerName sym3.local
    ServerAlias sym3.local
	SetEnv sfEnv dev

	#For Linux
    DocumentRoot /home/nntuan/Gits/sym3/web
	#For Windows
    #DocumentRoot D:/projects/sym3/web

	#For Linux
    <Directory /home/nntuan/Gits/sym3/web>
	#For windows
    #<Directory D:/projects/sym3/web>
        #Options Indexes FollowSymLinks
        AllowOverride all
        Require all granted
        <IfModule mod_rewrite.c>
            RewriteEngine On
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteRule ^(.*)$ app.php [QSA,L]
            RewriteCond %{HTTP:Authorization} ^(.*)
            RewriteRule .* - [e=HTTP_AUTHORIZATION:%1]
        </IfModule>
    </Directory>
    #For Ubuntu apache config
    ErrorLog ${APACHE_LOG_DIR}/error-sym3.log
    CustomLog ${APACHE_LOG_DIR}/access-sym3.log combined

    #For Xampp windows config
    #ErrorLog "logs/error-sym3.log"
    #CustomLog "logs/access-sym3.log" combined
</VirtualHost>
```

#Commands
```
tail -f -n 100 /var/log/apache2/access-sym3.log
tail -f -n 100 /var/log/apache2/error-sym3.log

php bin/console
php bin/console cache:clear --env=dev

php bin/console assets:install --symlink web
php bin/console assetic:dump --env=dev

php bin/console doctrine:migrations:diff --env=dev
php bin/console doctrine:migrations:migrate 20160321225157 --env=dev

php bin/console generate:bundle --namespace=TuanQuynh/UserBundle --dir=src --format=annotation --no-interaction

php bin/console doctrine:generate:entities AppBundle/Entity/User
php bin/console doctrine:schema:update --force

php bin/console app:add-user
```
