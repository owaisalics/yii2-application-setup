# Installing Yii 2.0 application
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

# DB Connection
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
http://localhost/practice/ows-application/frontend/web/index.php?r=site%2Fsignup 

And create a user with 
username: testuser
password: testuser

Now, you can login into the application using these credentials.


# Enabling Pretty URLs 

Currently, the URL looks like:
http://admin.ows-application.com/index.php?r=site%2Flogin
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

# Virtual Hosts 
Copy the the following in your httpd-vhosts file, most likely on 'xampp\apache\conf\extra\httpd-vhosts'
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

# Installing AdminLTE Theme in Yii 2.0 Application
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

Follow similar steps for the backend application if you want to enable the adminLTE theme in backend application.



Tutorial ends here

----














<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Yii 2 Advanced Project Template</h1>
    <br>
</p>

Yii 2 Advanced Project Template is a skeleton [Yii 2](http://www.yiiframework.com/) application best for
developing complex Web applications with multiple tiers.

The template includes three tiers: front end, back end, and console, each of which
is a separate Yii application.

The template is designed to work in a team development environment. It supports
deploying the application in different environments.

<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Yii 2 Advanced Project Template</h1>
    <br>
</p>

Yii 2 Advanced Project Template is a skeleton [Yii 2](http://www.yiiframework.com/) application best for
developing complex Web applications with multiple tiers.

The template includes three tiers: front end, back end, and console, each of which
is a separate Yii application.

The template is designed to work in a team development environment. It supports
deploying the application in different environments.

Documentation is at [docs/guide/README.md](docs/guide/README.md).

[![Latest Stable Version](https://img.shields.io/packagist/v/yiisoft/yii2-app-advanced.svg)](https://packagist.org/packages/yiisoft/yii2-app-advanced)
[![Total Downloads](https://img.shields.io/packagist/dt/yiisoft/yii2-app-advanced.svg)](https://packagist.org/packages/yiisoft/yii2-app-advanced)
[![Build Status](https://travis-ci.org/yiisoft/yii2-app-advanced.svg?branch=master)](https://travis-ci.org/yiisoft/yii2-app-advanced)

DIRECTORY STRUCTURE
-------------------

```
common
    config/              contains shared configurations
    mail/                contains view files for e-mails
    models/              contains model classes used in both backend and frontend
    tests/               contains tests for common classes    
console
    config/              contains console configurations
    controllers/         contains console controllers (commands)
    migrations/          contains database migrations
    models/              contains console-specific model classes
    runtime/             contains files generated during runtime
backend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains backend configurations
    controllers/         contains Web controller classes
    models/              contains backend-specific model classes
    runtime/             contains files generated during runtime
    tests/               contains tests for backend application    
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
frontend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains frontend configurations
    controllers/         contains Web controller classes
    models/              contains frontend-specific model classes
    runtime/             contains files generated during runtime
    tests/               contains tests for frontend application
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
    widgets/             contains frontend widgets
vendor/                  contains dependent 3rd-party packages
environments/            contains environment-based overrides
```
