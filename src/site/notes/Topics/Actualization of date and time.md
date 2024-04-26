---
{"dg-publish":true,"permalink":"/topics/actualization-of-date-and-time/"}
---


Whenever any actions are taken in the comparison page like connect, paste, connect edit, paste edit, comment/footnote/ non secure/ marking operations etc or in the import page, the latest time and date in the materia medica and import tables are displayed.

  

Technical Help:

  

For updating of time “updateDateOfModifiedSources()” PHP function is used, this function takes the “quelle_id” as parameter  and make changes in the “stand” field of the “quelle_import_master” SQL table.

  

Related PHP scripts:

  

- add-source-translation.php
    
- comparison.php
    
- comparison-super.php
    
- connect-edit-operation.php
    
- connect-swap-opearation.php
    
- connection-delete-script.php
    
- connection-save-script-earlier.php
    
- connection-save-script.php
    
- functions.php
    
- paste-edit-operation.php
    
- update-marking-symptoms.php
    
- update-symptom-info-comparison-table.php