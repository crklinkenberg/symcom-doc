For testing PHP Unit is used.
Test folders are present inside both the `symcom-core-app` and `symcom-laravel-app` directories.

#### PHP Test functions for Core PHP application located inside:
`symcom-core-app/tests`

#### PHP Test functions for PHP `Laravel` application located inside:
`symcom-laravel-app/tests`

A single `phpunit.xml` file is used for referencing both the tests directories. This file is located inside `symcom-laravel-app` directory.

Please ensure correct ownership and permissions are enforced to the above `tests` directories otherwise the tests would fail or not run successfully.

```
# Check permissions:
ls -l tests

# Enable full permission
chmod -R 777 tests
```

To run PHP unit test, use the below command inside `symcom-laravel-app` folder which can be accessed inside the docker container:
```
php artisan test
```
