---
{"dg-publish":true,"permalink":"/conversion-of-grading-during-display/"}
---

#general #comparison 

Symptoms displayed on Symcom program are displayed in different text formats/ grades and this is the effect of Gradings assigned to the source or to specific symptoms in the program.

Basic Workflow is mentioned here:
1. The `convertTheSymptom()` PHP function is responsible for affecting the grades of the symptoms during display.
2. Punctuations are fixed from the symptom string. More on this: [[Topics/Punctuation removal from grading\|Punctuation removal from grading]]
3. All custom HTML tags (which are present in the symptom strings saved in the database) and their converted form are kept in `conversionArr`. 
4. Bracketed part of the string which is imported as "part of symptom" is affected by grading, hence it is processed.
5. The global grade values assigned are taken out from SQL tables `global_grading_set_values` and `global_grading_sets` and kept in `globalGradingSignArr` with the grade format as its key and is kept in `globalGradingArr`. 
```PHP
//Example:
//if formatGrade fetched from SQL row is 3.
//if formatCustomSign for that row is "strong".
$globalGradingSignArr[$formatGrade] = $formatCustomSign;
//result:
$globalGradingSignArr[3] = "strong";
```
6. The grade settings for the symptom is first fetched from the source via `quelle_grading_settings` SQL table and if symptom specific grades are assigned then it is fetched from `symptom_grading_settings` SQL table.
7. If edit preview `isEditPreview` flag is active, which is the flag for showing the converted form when CE is done then the grade setting is fetched from `temp_editable_symptom_grading_settings` SQL table.
8. All the grade setting fetched are kept in `sourceSettingData`.

Below is an illustration on how symptoms will react when `kursiv` grades are converted from grade setting. This is done for each grade which have been assigned a setting.
```PHP
//Example:
//For kursiv option if 3 is assigned in the grade setting, then.
$sourceSettingData['kursiv'] = 3;
$kursiv = $sourceSettingData['kursiv'];
//The global grade for 3 is fetched from global grading array.
$key = $globalGradingArr[$kursiv];
//For kursiv, the symptoms are saved in the database with custom HTML tag "non-asterisk-degree-em".
//We make changes in the conversionArr.
$conversionArr['non-asterisk-degree-em'] = $key;
//Since globalGradingArr[3] = "strong", so non-asterisk-degree-em will be assigned "strong"
//Result
$conversionArr['non-asterisk-degree-em'] = "strong";
```

9. If `includeGrade` input parameter is active, grade numbers are attached to the symptom string.
10. The `conversionArr`is finally processed and the key of this array is searched in the symptom string and is then replaced with the values of this array in the symptom string.
11. Final manipulation and cleaning is done and the finalized converted symptom string is then returned by the program.