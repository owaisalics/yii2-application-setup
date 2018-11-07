# Yii 2.0 application
[![Contribution Open](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/ows-ali/yii2-application-setup/blob/master/CONTRIBUTING.md)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ows-ali/yii2-application-setup/issues)

## Contribution
This repository is open for contributions including solving any issue, creating your own issue or creating a pull request etc

## Installing the project
First run this command in cmd:
````
composer create-project --prefer-dist yiisoft/yii2-app-advanced ows-application
````
The application will be installed in 'ows-application' directory. You can rename it according to your project name

Then, run the command:
````
init
````
and choose 'dev' to initialize the application in development environment.

## DB Connection with MySQL
To change the MySql Database name, go to common/config/main-local.php
and set dbname to
 ````
 'ows_database' 
 ````
(and edit the username and password if you have changed them)

Now, run the command 
````
yii migrate
````
This will generate the user table in your database.

Now, Go to 
http://localhost/ows-application/frontend/web/index.php?r=site%2Fsignup 

And create a user with 
username: testuser
password: testuser

Now, you can login into the application using these credentials.


## Enabling Pretty URLs 

Currently, the URL looks like:
http://localhost/ows-application/backend/web/index.php?r=site%2Flogin
but we want it to be as follows:
http://localhost/ows-application/backend/web/login
In order to enable pretty URLs, go to backend\config\main.php and uncomment the following code in $components['urlManager'] (do not forget to add the rules):

````
'urlManager' => [
            'enablePrettyUrl' => true,
            'showScriptName' => false,
            'rules' => [
                '<alias:\w+>' => 'site/<alias>',
            ],
        ],

````

Make a .htaccess file with the following code and place it in backend/web folder:

````
RewriteEngine on

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php
````

Do the same in frontend application.

## Virtual Hosts 
Copy the following in your httpd-vhosts file, most likely on 'xampp\apache\conf\extra\httpd-vhosts'
(Make sure to change the DocumentRoot to set it as your own web root directory)

````
<VirtualHost *:80>
       ServerName admin.ows-application.com
       DocumentRoot "E:\xampp\htdocs\ows-application\backend\web"
</VirtualHost>

<VirtualHost *:80>
       ServerName ows-application.com
       DocumentRoot "E:\xampp\htdocs\ows-application\frontend\web"
</VirtualHost>
````

and the following in your hosts file at C:\Windows\System32\drivers\etc (you may be required to open the file in Administrator mode):

    
    127.0.0.1       admin.ows-application.com
    127.0.0.1       ows-application.com


Restart your Apache server.

Now, you can access your backend and frontend applications on admin.ows-application.com and ows-application.com respectively.

## Installing AdminLTE Theme in Yii 2.0 Application
Run the following command

    composer require dmstr/yii2-adminlte-asset "^2.1"

Now, go to frontend/config/main.php and add this in components['view']

````
'view' => [
            'theme' => [
                'pathMap' => [
                    '@app/views' => '@vendor/dmstr/yii2-adminlte-asset/example-views/yiisoft/yii2-app'
                 ],
             ],
        ],
````

Follow similar steps for the backend application if you want to enable the AdminLTE theme in backend application.

## LICENSE
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://github.com/ows-ali/yii2-application-setup/blob/master/LICENSE)
