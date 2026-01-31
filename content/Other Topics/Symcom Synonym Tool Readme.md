### Important Details:
Git repo link: `https://github.com/crklinkenberg/symcom-synonym-tool.git`

### Local Setup Guidelines
#### Download XAMPP 7.1.33: 
`https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/7.1.33/xampp-windows-x64-7.1.33-1-VC14-installer.exe/download`

```
Add XAMPP installation location to Path in environment variables.

C:\xampp\php to Path in environment variables if not already done.
```


#### Download Composer Phar 1.6.3: 
`https://getcomposer.org/download/1.6.3/composer.phar`

Navigate to `htdocs` directory inside `XAMPP installtion directory` and clone Git repo: 
`Link`

The whole project will now contain under `symcom-synonym-tool` folder which is the root directory of the cloned project.

Copy `composer.phar` to the cloned directory (root).
Install dependencies using the below commands in terminal.
```
php composer.phar show
php composer.phar install
```

Copy `composer.phar` to  `symcom-synonym-tool\symcom\api`.
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
#### Database and Routing Setup
Open the project folder in a code editor and navigate to `symcom-synonym-tool/config/route.php` and change the PHP variable `$dbName` to a desired database name. Example: `new_database_synonym_test`.

In this file change the PHP variable `$absoluteUrl` to `http://localhost/symcom-synonym-tool`. Here `symcom-synonym-tool` is the root directory of the cloned project.

Navigate to `symcom-synonym-tool/symcom/api` and copy all contents of `.env.example` file to a new `.env` file. Change the `DB_DATABASE` value to the new database name defined. Example: `new_database_synonym_test`.

Navigate to `symcom-synonym-tool/symcom/api/config/constants.php` and make sure the PHP value for `$configArray2 ['api_base_path']` is set to `http://localhost/symcom-synonym-tool/symcom/api/public/`.


#### Running the program
Open XAMPP control panel `xampp installtion directory/xampp-control.exe` and start `Apache` and `MySQL` services.

Create a new database with name defined in the project files mentioned above. Example: `new_database_synonym_test`. Can be doe with `phpmyadmin` by going to `http://localhost/phpmyadmin/` site in the browser or any other database management tools.

Import the given database to this newly created database. Once database import is complete, the project can be opened at `http://localhost/symcom-synonym-tool/` URL in the browser.

<hr>

# Inside the Symcom Program
Log in using credentials:
```
username: guest
password: guest123
```

