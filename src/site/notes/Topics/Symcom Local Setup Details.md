---
{"dg-publish":true,"permalink":"/topics/symcom-local-setup-details/"}
---

# Prerequisites

 + **Windows Operating System**
 + **XAMPP 7.1.33**
 + **PHP Ver. 7.1 - 7.2**
 + **Composer 1.6.3**


Testingggggg.

#### Download XAMPP 7.1.33: 
`https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/7.1.33/xampp-windows-x64-7.1.33-1-VC14-installer.exe/download`

```
Add XAMPP installation location to Path in environment variables.

C:\xampp\php to Path in environment variables if not already done.
```

#### Download Composer Phar 1.6.3: 
`https://getcomposer.org/download/1.6.3/composer.phar`

Navigate to `htdocs` directory inside `XAMPP installtion directory` and clone Git repo: 
`https://github.com/crklinkenberg/symcom01.git` which is the development link for Symcom.

The whole project will now contain under `symcom01` folder which is the root directory of the cloned project.

Copy `composer.phar` to the cloned directory (root).
Install dependencies using the below commands in terminal.
```
php composer.phar show
php composer.phar install
```

Copy `composer.phar` to  `symcom01\symcom\api`.
Install dependencies using the below commands in terminal.
```
php composer.phar show
php composer.phar install
```

Once all dependencies are installed, it is advised to modify the `php.ini` variables.
```
Go to your xampp installation directory -> php -> (open) php.ini file and make these changes.
    max_execution_time = 12000.
    max_input_time = 6000.
    memory_limit = 1024M.
    upload_max_filesize = 100M.
    post_max_size = 100M.
```

Start XAMPP server.

Open XAMPP installed directory and open xampp-control.exe as Administrator. Example ```C:/xampp/xampp-control.exe```

Click  start button for both Apache and MySQL and wait until they turn green and then after that follow the instructions below.

Database can be accessed from `http://localhost/phpmyadmin/` in the browser.

Create new database and  import the database extracted from AWS or SQL provided.
```
To import data via terminal:
In XAMPP control panel, ind a button named **Shell** in the right hand side and click that button and then use the following command:

mysql -u root -p my_database < "location of the .sql file"
```
Command Help:
```
root : is database username
-p : stands for password which is blank by default
my_database : is the database which we created in the http://localhost/phpmyadmin/
"location of the .sql file" : should be the path of the .sql file that you have with you to import

Example: mysql -u root -p my_database < "C:/Users/Mypc/Downloads/development_repertory.sql
```

# Installation

Go to your project directory. Example: ```C:/xampp/htdocs/symcom01```, delete the existing `.htaccess` file and then rename `.htaccess-local` to `.htaccess`.

Change the configuration in the mentioned location: `config/route.php`
Open this file with an editor and change the database configuration with your details: 
```
$dbUsername = 'root'; // The default Xampp database username is root.
$dbPassword = ''; // The dufault Xampp database pasword is blank.
$dbName = 'my_database_name';  
```

In this file change PHP variable `$absoluteUrl` value to your application URL. 
Example: `http://localhost/symcom01/`. Here `symcom01` is the git cloned directory name which is also the project root. 
```
Change:
$absoluteUrl = (isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] === 'on' ? "https" : "http") . "://$_SERVER[HTTP_HOST]/";

To:
$absoluteUrl = "http://localhost/symcom01/";
```
   

Inside `C:/xampp/htdocs/symcom01/dev-exp/` directory delete the existing `check-if-comparison-table-exist.php` page and then rename `check-if-comparison-table-exist-local.php` page to `check-if-comparison-table-exist.php`.

Follow the steps below for the location: ```C:/xampp/htdocs/symcom01/symcom/api```
   - Delete the existing `.env` file and then rename `.env.development` to `.env` on current location.
   - Open this `.env` file with an editor and change the database details just like above:
```
DB_DATABASE=my_database_name
DB_USERNAME=root
DB_PASSWORD=
```


Open file ```constants.php``` in an editor, go to the location: ```C:/xampp/htdocs/symcom01/symcom/api/config/constants.php```

```
Change:
if (app()->environment('development')) {
	$configArray2 ['api_base_path'] = 'http://dev.reference-repertory.com/symcom/api/public/';  
}

To:
if (app()->environment('development')) {
	$configArray2 ['api_base_path'] = 'http://localhost/symcom01/symcom/api/public/';  
}
```
   
After successful changes, the application can be opened in browser with URL: `http://localhost/symcom01/`.


