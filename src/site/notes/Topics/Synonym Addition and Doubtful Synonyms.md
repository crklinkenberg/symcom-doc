---
{"dg-publish":true,"permalink":"/topics/synonym-addition-and-doubtful-synonyms/"}
---


When synonyms are added, the references for these synonyms are mandatory in the new insertion  form. Doubtful synonyms or doubtful references are displayed with yellow background color in the synonym list. Doubtful synonyms do not take part in import and comparison process. Only after resolving of these doubtful synonyms by the supervisor, these synonyms takes part in import and comparison process.

Technical Flow:

Lumen API is used for this process.  Views are contained inside “Stammdaten” directory. “SynonymDeController” and “SynonymEnController” are the controllers.

Inputs are taken from the form and inserted in SQL table.

Related sql tables:

- synonym_de
    
- synonym_en
    
- synonym_de_synonym_reference
    
- synonym_en_synonym_reference
    
- synonym_reference
    

  

Related Scripts:

1. assets/js/formValidation.js
    
2. SynonymEnController.php
    
3. SynonymDeController.php
    
4. stammdaten\synonym-en\add.php
    
5. stammdaten\synonym-en\edit.php
    
6. stammdaten\synonym-de\add.php
    
7. stammdaten\synonym-de\edit.php