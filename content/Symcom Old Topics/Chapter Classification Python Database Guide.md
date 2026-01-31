---
{"dg-publish":true,"permalink":"/topics/chapter-classification-python-database-guide/"}
---


# Connect custom MySQL Server

The described set-up is the most user-friendly way to create a local MySQL Server to back the application on. It consists of creating a Docker MySQL Container Server, and connecting it to MySQL Workbench and work from there.

## Prerequirements

- Have [Docker](https://docs.docker.com/engine/install/) installed.
- Have [MySQL Workbench](https://dev.mysql.com/doc/workbench/en/wb-installing.html) installed(MySQL Workbench 8.0 CE recommended).

## Set up Database Locally in Docker Container

### BE AWARE FOR PRODUCTION!!

If container is deleted entire database will be lost. It is suggestable to have MySQL database in local system and have periodical back-ups.

1. Create MySQL container server using:

```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=<password> -p 3307:3306 -d mysql:8.0.36
```

#### On MySQL Workbench:

2. Next to "MySQL Conections" click on "+".
3. Type "MySQLContainerServer" for "Connection Name".
4. Change "Port" to "3307".
5. Click on "OK".
6. The password for the "root" user is the previous value of "\<password>".
7. Double-click on the "MySQLContainerServer" instance.
8. Click on "Server" on the top menu.
9. Click on "Data Import".
10. Select "Import from Self-Contained File".
11. Click on "..." and select [databaseDump.sql](./databaseDump.sql).
12. Next to "Default Target Schema" click on "New...".
13. Type "symptom_classification" and click on "OK".
14. Click on "Start Import".
15. If application will be run from Docker container set "host" to "host.docker.internal", else set it to "localhost".
16. Go to [databaseCredentials.py](../restServer/dataProcessing/util/databaseCredentials.py) and change line 3 to the following parameters:

```bash
...nectToMySQL(user="root", password="<password>", host="<host>", port=3307)
```
