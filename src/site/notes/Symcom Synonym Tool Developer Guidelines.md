---
{"dg-publish":true,"permalink":"/symcom-synonym-tool-developer-guidelines/"}
---


## Local machine set-up:


```
== Tools Required ==
Windows OS
MySQL WorkBench
XAMPP 7.1.33
PHP Ver. 7.1 - 7.2
Composer 1.6.3
```

The developers will be added as collaborators in the project repo.

Clone the git repo `https://github.com/crklinkenberg/symcom01.git`.
Switch to remote branch `synonym-tool`.

*Instructions for setting up using XAMPP and composer in Windows OS will be given here. *

##### Database setup:
Database for running Symcom locally will be provided along with the set-up. This database will contain all required SQL tables including  symptoms which should be used for the new tool implementation. At any point of time, if new symptoms are required to be tested with the tool, the database will be provided again.

*Instructions for setting up the MySQL database, including already existing symptoms, synonyms, stop words SQL tables will be given here.* 

Once local server is running and the project files are opened in a code editor. Navigate to `synonym-tool` folder. This will be the working directory for new synonym tool implementation. Any dependencies for the program, new PHP scripts should be created inside this directory.

Only contents inside `synonym-tool` directory from `synonym-tool` branch will be considered for integration with the Symcom program during merging.


## Inside Symcom Program:

Log in using credentials:
```
username: guest
password: guest123
```

*The basic work flow will be detailed here. How the synonym tool classification would start, which icon will be clicked and which backend script will be responsible will be given here.*

![Pasted image 20250110135137.png](/img/user/assets/Pasted%20image%2020250110135137.png)

## Synonym Tool on completion:

After successful completion of the program, the `synonym-tool` branch will be merged. This will be done after complete review and removing any code conflicts.