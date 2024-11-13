---
{"dg-publish":true,"permalink":"/topics/synonym-addition-and-doubtful-synonyms/"}
---

#general 

When synonyms are added, the literatures for these synonyms are mandatory in the new insertion  form. Doubtful synonyms or doubtful literatures are displayed with yellow background color in the synonym list. Doubtful synonyms do not take part in import and comparison process. Only after resolving of these doubtful synonyms by the supervisor, these synonyms takes part in import and comparison process.

### Technical Flow:

Laravel API is used for this process.  Views are contained inside “Master Data” directory. `SynonymController.php` is responsible for any changes. English and German versions can be controlled sending the input parameters. 

Inputs are taken from the form and inserted in SQL table.
```
Related sql tables:
- synonym_de
- synonym_en
- synonym_de_synonym_reference
- synonym_en_synonym_reference
- synonym_reference
```
  
Related Scripts:
```
1. assets/js/formValidation.js
2. SynonymController.php
3. master-data\synonym-en\add.php
4. master-data\synonym-en\edit.php   
5. master-data\synonym-de\add.php   
6. master-data\synonym-de\edit.php
```

Additional Details: [[Topics/Symcom Master Data Guide, API included\|Symcom Master Data Guide, API included]]
