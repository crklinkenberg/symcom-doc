---
{"dg-publish":true,"permalink":"/symcom-v2-documentation/project-structure/"}
---


```
project-root
|-db-setup
|-master-data-openapi
|-symcom-core-app
|-symcom-laravel-app
```

All files related to core PHP application can be found inside `symcom-core-app` directory.
All files related to PHP `laravel` application can be found inside `symcom-laravel-app` directory.

The whole application is built with core PHP, but the API for master-data including the user login/signup are built using PHP `Laravel` framework.

The `master-data-openapi` directory contains `yml` files which includes documentation for the API.

The database setup, SQL files are present inside `db-setup` directory. The installation details of these SQL tables to the docker MySQL database is available in [[symcom-v2-documentation/Local Setup Guidelines\|Local Setup Guidelines]].

