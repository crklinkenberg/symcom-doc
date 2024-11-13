---
{"dg-publish":true,"permalink":"/topics/editor-abbreviation-column-in-import-and-materia-medica/"}
---


In our current application, the initials of editors can be added or updated from the "user" menu point in Symcom program, these initials will get saved into the system and reflect in the Materia medica and import pages whenever any changes or modifications are made to the source or a comparison. For log in with "admin" credentials, the initial is taken as “ADMIN" by the program.

PHP function `getUserInitialFromId()` is used to get the editor initials or abbreviation. The input parameter should be the user ID.

NOTE: It is always recommended to follow the PHP script `functions.php` for proper syntax and parameter selection of all the PHP functions in this documentation.