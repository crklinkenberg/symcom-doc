---
dg-publish: true
---

### Technical Guide
#### Bonnighuasen Rubrick Headings
Bonnighuasen Rubrick headings are imported first. The script associated is `import-bonninghausen-rubick-headings.php` present under `symcom-core-app\dev-exp\`.

Upon submission of text from the browser:
1. All symptoms are deleted from `bonninghausen_symptoms` SQL table.
2.  Each input line is scanned one by one and it is similar like the import process of symptoms where each line is processed and stored in `variablesArray` PHP array with appropriate fields and is then inserted in the SQL table.
3. The `rawLineForBonninghausen` field in the `variablesArray` stores the exact line as it is present in the Word document.
4. All processing of the string is done via `importedStringManipulationProcessForBonninghausen()` PHP function. This function is almost similar in structure like the `importedStringManipulationProcess()` function.
5.  To identify the string as a Bonnighausen string, it is searched via regex inside the above function. The function returns  `variablesArray` and it is then inserted into `bonninghausen_symptoms` SQL table. The gradings are saved in `bonninghausen_symptom_grading_settings` SQL table.

The imported rubrick headings are displayed in `bonninghausen-symptoms.php` script which is present under  `symcom-core-app\dev-exp\`.


#### Bonnighausen Headings
Upon submission of text from the browser:
1. The settings for the import is stored in `bonninghausen_import_settings` SQL table. If settings already present for the medicine, then it is not imported. 
2. Each line sent is scanned one by one and PHP function `importedStringManipulationOfBonninghausenHeading()` processes the whole string same like the import process function `importedStringManipulationProcess()`.
3. The `importedStringManipulationOfBonninghausenHeading()` function cleans the heading provided and stores in `bonninghausenCleanHeading` field of the `variablesArray` PHP array. It is then searched and compared for existence in `bonninghausen_symptoms` SQL table. If heading is found, the line scanned is saved in `bonninghausen_approved_symptoms` SQL table. If no match is found then it is stored in `bonninghausen_re_importable_headings` SQL table.

Conditions for acceptance of Bonnighausen headings:

1. The string must have roman numerals in it in the starting. The match is done programmatically via regex.
2. Presence of "-" in the starting of the string.
3. The heading after processing from `importedStringManipulationOfBonninghausenHeading()` PHP function, should find a match in `bonninghausen_symptoms` SQL table.
4. If same heading appears twice but the initial content contains pattern like `bttb` or `++bttb`, then the one having "+" will be accepted. If the pattern is same for heading like `bttb`, then the number inside curly braces in the string is compared and the one having highest number is accepted. For these string operations PHP function `operateDuplicateBonnighausenHeadeings()` is involved.
   
Pre-processing of strings for acceptance:
1. The strings if contains patterns like `++bttb, +++bttb++, +++bttb+P` etc. are operated and anything before this pattern is removed to extract the heading.
2. The input line containing is also stored in its raw form in field `bonnighausen_raw_line` of the `bonninghausen_approved_symptoms` SQL table as it is later used by `operateDuplicateBonnighausenHeadeings()` PHP function to accept the appropriate heading while importing.

#### Approved and Unapproved Heading List
The approved list is shown in `bonninghausen-approved-symptoms.php` script and the unapproved list is shown in `bonninghausen-un-approved-heading.php`, both of which are present inside `symcom-core-app\dev-exp\`.

The displaying workflow is same like the `symptoms.php` page when viewing symptoms.

#### Transfer of approved bonnighausen symptoms to import database

Brief Workflow:
1. HTML class `transfer-btn` is responsible to initiate the whole transfer process. The associated JavaScript code is present in `import-bonninghausen.php` script.
2. The backend script `bonninghausen-symptoms-transfer-to-main-import.php` is connected via ajax and imported setting id is sent via POST.
3. Inside this script, the setting is retrieved from the id sent and the approved symptoms associated with the id is taken out from  `bonninghausen_approved_symptoms` SQL table. The grade setting is also taken from `bonninghausen_approved_symptom_grading_settings` SQL table.
4. The selected data are then inserted into `symptom_grading_settings` and `symptoms` SQL table.

#### Export of Bonnighausen data to csv file
The script associated is `bonnighausen-export-excel.php` present inside `symcom-core-app\dev-exp\`.

The default text to csv from PHP is used inside this script. Data taken out from `bonninghausen_approved_symptoms` table is written in a csv which gets downloaded in the browser.








