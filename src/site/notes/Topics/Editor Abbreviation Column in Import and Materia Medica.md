---
{"dg-publish":true,"permalink":"/topics/editor-abbreviation-column-in-import-and-materia-medica/"}
---


In our current application, the initials of editors can be added or updated from the "user" menu point in Symcom program, these initials will get saved into the system and reflect in the Materia medica and import pages whenever any changes or modifications are made to the source or a comparison. For log in with "admin" credentials, the initial is taken as “ADMIN" by the program.

  

PHP function “updateLatestEditorInitials()” is used for performing this operation. This function takes the editor initial (string), the quelle id of the comparison and a flag(int) as parameters. The values of this flag:

  

1. 1 => for operations in comparison related scripts.
    
2. 2 => for operations in import processes.
    

The scripts related to this operation are all similar to the time and date modification process.

  

NOTE: It is always recommended to follow the PHP script “functions.php” for proper syntax and parameter selection of all the PHP functions in this documentation.