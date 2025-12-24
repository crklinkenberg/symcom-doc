---
{"dg-publish":true,"permalink":"/symcom-v2-documentation/local-setup-guidelines/"}
---


Clone the git repository.

<hr>

# Prerequisites:

```
Git
Composer 2.8.3
Docker version 26.1.3
Docker Compose version 2.27.1
```

# Installation steps:
Step 1: 
Run Docker using below command from project root directory. This will install `PHP` in `apache` environment and `MySQL` in two separate containers. Containers will be named `syncom-app` and `db`. All dependencies will be installed.
 
```
docker compose build --no-cache
```

Step 2:  
After build is successful, run the docker containers.

```
docker compose up -d
```

Step 3: 
Make three instances of the terminal. One instance with current working directory as the project root. 
In second instance, go inside the `symcom-app` container using:

```
docker exec -it symcom-app bash
```

In third instance, go inside the `db` container using:
```
docker exec -it db bash
```

Log in to MySQL inside `db` container:
```
mysql -u root -p
Password
```
Then use database: `symcom_db`.
```
use symcom_db;
```

Step 4: 
Go to the `symcom-app` container,
Navigate to `symcom-laravel-app`.
Install composer dependencies. `composer install --no-dev --optimize-autoloader`. The `vendor` folder will display upon successful installation.

Step 5: 
The `docker-compose.yml` file has database values:

```
MYSQL_ROOT_PASSWORD: root
MYSQL_DATABASE: symcom_db
MYSQL_USER: user
MYSQL_PASSWORD: password
```

Create a `.env` file in `symcom-laravel-app`, copy contents from `.env.example` script and replace the below values:

```
DB_HOST=db # the container's name from docker-compose.yml file
DB_DATABASE=symcom_db
DB_USERNAME=user
DB_PASSWORD=password
```

Step 6: 
From the project files, go to `symcom-core-app/config/route-sample.php` and rename it to `route.php` and do the below changes:

```
$dbHost = 'db'; # the container's name from docker-compose.yml file
$dbUsername = 'user';
$dbPassword = 'password';
$dbName = 'symcom_db';
```

Then, navigate to `symcom-core-app/dev-exp/db-connection-pool-sample.php` and rename it to `db-connection-pool.php` and do the same changes as mentioned above.

Step 7: 
In the project root terminal instance, navigate to `db-setup` directory. Execute the below command:
```
cat new_symcom.sql | docker exec -i db mysql -u root -proot symcom_db
```

This will dumb the SQL data to the `symcom_db` database.
Here `symcom_db` is the database name, if it is changes, the new database name should be provided.

Step 9: 
In the terminal instance of `symcom-app` container, navigate to `symcom-laravel-app` inside the container.

Execute:

```
php artisan key:generate
```

This will generate `APP_KEY` which can be found in the `.env` file.

Step 10: 
Then, execute migrations command for `laravel`:

```
php artisan migrate
```

This will install `oauth` SQL tables used by `passport` from `laravel` for authentication.

Step 11: 
Then, inside the container, generate `laravel` passport keys which are used in the authentication process:

```
php artisan passport:keys
```

This will create `.key` file inside the `storage` directory inside the container.

Step 12:
Then, inside the container give permission to `laravel` files created:

```
chown -R www-data:www-data storage bootstrap/cache 
```

```
chmod -R 775 storage bootstrap/cache 
```

```
find storage -type f -name "oauth-*.key" -exec chmod 600 {} \;
```

Step 13:
Go to the terminal instance of `db` container:
Check if personal access token is present in database inside the `mysql` container:

```
SELECT * FROM oauth_clients WHERE personal_access_client = 1;
```
If not present, navigate to `symcom-laravel-app` and create one using:
```
php artisan passport:client --personal
```
Check `oauth` SQL table again:
```
SELECT * FROM oauth_clients WHERE personal_access_client = 1;
```

Step 14: 
From the project root terminal instance, navigate to `symcom-core-app` and rename `.htaccess-local` to `.htaccess`.

# Routing

Once the build is successful and docker containers are running, the application can be accessed at `http://localhost/` when running in local environment. 

The `apache` `.conf` file routes core PHP codes to `symcom-core-app` directory and API links with prefix `api-link` to `symcom-laravel-app` directory. Hence, the back-end links should be like this: `http://localhost/api-link/login` for endpoint `login`.

# Troubleshoot:
```
If new database is not created after docker compose build, use:
docker compose down -v

This will remove any volume previously built and new database will be created.
Alternatively bash to backend database container after docker built and run is successful using:

docker exec -t db bash

This takes inside the db container.

Run: mysql -u root -p

This will log in to mysql using root access. Root password is root.

Then see all databases using: SHOW DATABASES;

The new database should be created and if not, then create a new database using mysql CLI commands.

*** In order to view any tables and select rows other CLI actions can be performed here. ***
```

