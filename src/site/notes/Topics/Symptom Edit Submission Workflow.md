---
{"dg-publish":true,"permalink":"/topics/symptom-edit-submission-workflow/"}
---


```
1. When symptom edit modal is submitted via HTML class "symptom-edit-modal-submit-btn", it is handled by "symptom-icon-function.js" script.
2. It is then sent to "update-symptom-and-settings-comparison-table.php" script via ajax.
3. After processing of the string in the above mentioned script it is handled by PHP function storeEditedSymptom(). This function updates in the completed table if only converted version is modified, or updates to both completed and quelle_import_test table if original version is modified. 
4. The original version column in SQL table is BeschreibungOriginal_de and converted version column is BeschreibungFull_de.
5. Then modifiyGradingSettingsForTheSymptom() PHP function is called from the update script which saved the grading to symptom_grading_settings SQL table. The symptom type is saved to symptom_type_setting table.
```