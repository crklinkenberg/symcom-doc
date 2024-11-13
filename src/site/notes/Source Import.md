---
{"dg-publish":true,"permalink":"/source-import/"}
---

#import
### Technical Workflow:
1. Import of source is done via main web page `source-import/import.php` script which holds the main UI for importing of symptoms to particular book or magazine.
2. On submission of the import HTML form, it is first validated by JS function `importSource()` and on successful validation the HTML form with its ID `source_import_form` is submitted. 
3. It is then processed by `source-import/onsubmit-import-process.php` where it first checks if the import setting is already exists and if it exists error is reported to the user, else the script proceeds to the next lines of codes.
4. Insertion of import setting and tester relationship in the temporary tables is done. Tables involved:
```
itemp_import_source_settings
rel_itemp_import_source_setting_tester
```

##### Import String Manipulation Function:
5. The lines pasted in the text editor are kept in `symptomsArray` and each line is passed through `importedStringManipulationProcess()` PHP function for deep string scanning and processing.
6. Check for pre defined reference is done. Checks `literature start` or `literatur start` in the line. It is controlled by flag `isPreDefinedReferenceSection`. More details on Allen Source Import Concept can be found here: [[Topics/Allen Source Import\|Allen Source Import]]
7.  Check for the first character of the line is done. Checks `@,(,[,` or if it is number.
8.  If no symptom description is found then the iteration among the line continues and next line is checked.
9. If symptom description is found, it is kept in `Beschreibung`. If a number is found with Symptom text then the line is further cleaned and the number is kept in `Symptomnummer` key of `variablesArray`.
10. When the symptom description is cleanly extracted, further operations are done. Check for first five character is done. Occurrence of theta is also detected. 
```
Important PHP functions involved:

convertPatternPortions(): This function detects the special symbol like *,θ,° etc. and returns the a string having customized HTML tag relating to the special symbol detected.

findTheOpenedTag(): Finds the opened HTML tag from a string part.

separateTheApplicableStratingSign(): Separates the special symbol and appends it in front of the symptom string with customized HTML tags.

structureNonAsteriskAndDegreePortions(): Add customized HTML tag "non-asterisk-degree" with the symptom string.

structureEndingWithDegreeFormatString(): Add customized HTML tag "endwithdegree" with the symptom string.

structureEndingWithSingleTFormatString(): Add customized HTML tag "endwithsinglet" with the symptom string.

structureEndingWithDoubleTFormatString(): Add customized HTML tag "endwithdoublet" with the symptom string.
```

11. If literature number is found, it is encapsulated under `sup` HTML tag.
12. Resolution of testers for literature source is done. The testers from literature source are kept in `prueferFromParray` key of `variablesArray`, this tester is then checked if already exists in the tester database and if not found, then check for approval flag remains active and it is kept in `prueferArray` key of `variablesArray` for further processing. Similar checks are done for source literature, medicines which are not present in the database and needs approval.
13. The whole flow is procedural approach so checks and resolutions are done for each cases one by one.
14. Last bracketed string, middle bracketed string are also checked tester, medicine or part of a symptom. Several cases exists for string case, all can be easily followed in the code script. Checks for comma, semi-colon, hyphen are also done.
15. The final string manipulation data is kept in `variablesArray` and is then returned by the function.
16. It is to be remembered that this string manipulation function runs for each element (lines) in the `symptomsArray` of the `onsubmit-import-process.php` script so the returned array from the `importedStringManipulationProcess()` PHP function will contain information on unapproved testers, literatures, medicines if found in any line, and at the end of the processed these are further processed for approval and saved into the master database.
##### Insertion in temporary tables:
17. Once the string is finished and returns from string manipulation function, different parts of the symptom string are taken out from `variablesArray` returned from the function and is then inserted into the `itemp_symptoms` SQL table. This is a temporary table where symptom information is kept when import of symptom is done. Other data are also inserted in the temporary tables.
```
Other SQL tables involved:
itemp_symptom_grading_settings
rel_itemp_symptom_tester
itemp_approved_testers
itemp_testers
rel_itemp_symptom_itemp_tester
rel_itemp_symptom_medicine
itemp_medicines
rel_itemp_symptom_itemp_medicine
rel_itemp_symptom_medicine
rel_itemp_symptom_literature
itemp_approved_literatures
itemp_literatures
rel_itemp_symptom_itemp_literature
rel_itemp_symptom_pre_defined_literature
rel_itemp_symptom_pre_defined_tester
```

##### Questioning process of unapproved temporary data of the symptoms:
18. Once insertion of all the symptoms data are done to the temporary tables, the `onsubmit-import-process.php` script is redirected to the `import.php` script where the program checks if any unapproved data is present in the temporary tables.
19. If unapproved data are found it is handled by `questioning-process-of-unapproved-temporary-symptoms.php` script. 
##### Transfer of temporary data to main tables:
20. Once all approval of temporary is complete, the data are then sent from temporary tables to main tables. `questioning-process-of-unapproved-temporary-symptoms.php` script handles this operation.
```
SQL tables involved:
itemp_symptoms
itemp_import_source_settings
import_source_settings
rel_itemp_import_source_setting_tester
rel_import_source_setting_tester
rel_source_medicine
symptoms
itemp_symptom_grading_settings
symptom_grading_settings
rel_itemp_symptom_medicine
rel_symptom_medicine
rel_itemp_symptom_tester
rel_symptom_tester
rel_itemp_symptom_literature
rel_symptom_literature
rel_itemp_symptom_pre_defined_literature
rel_symptom_literature
rel_itemp_symptom_pre_defined_tester
rel_symptom_tester
rel_itemp_import_source_setting_tester
sources
```
21. Once the transferring is complete, the data are deleted from the temporary tables and the import of symptoms to source operation is complete.