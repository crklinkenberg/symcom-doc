---
{"dg-publish":true,"permalink":"/topics/new-modification-in-normal-symptom-edit-ce-swap-ce/"}
---

#comparison 

We can normally edit a symptom form the symptom listing page of a source. While editing a symptom from the symptom listing page of the source, on clicking the edit icon button we get the symptom edit mask /popup.

Here in this popup according to our new modification, we are always providing the imported version of the symptom to edit in the textarea field. We have also displayed the original and converted version of the symptom just above the textarea field.

Here in the symptom edit popup we have a settings tab, in this settings tab user can set or modify the grading settings value for the editing symptom.

There is a filed add as Individual Upgrade justification where user can write their comment on Upgradation reasons.

Here user also have control over where the edit should get impacted, user have options to choose whether to edit both original and converted version or edit only converted version.

We have also introduced an edit preview phase, where the user can see the result of the edit, just before the final submission of the edit process. User can correct their mistake by clicking the Go back button from the preview phase.

**In case of CE, SWAP CE:**

Same as normal symptom edit process, in case of CE, SWAP CE connection also we provide the imported version of the symptom to edit in the textarea field. We have also displayed the original and converted version of the symptom just above the textarea field, in the CE or SWAP CE popup.

In this popup also we have the settings tab where user can set or modify the grading settings value for the CE or SWAP CE symptom.

Same way we also have the preview phase, where the user can see the result of the CE or SWAP CE edit, just before the final submission of the CE or SWAP CE process. Here also we can go back to correct our editing by clicking the go back button in the preview phase of the CE or SWAP CE popup. 

### **Technical Workflow:**

**Symptom edit:**

Symptom edit process also little bit same as the CE, SWAP CE process. When we click on the edit icon button we fetched symptom information/data from the database table with the help of PHP script “get-editable-symptoms.php” using AJAX and populate the fetched data in the symptom edit popup.

Here clicking on the Preview button of the symptom edit popup, we POST the popup from data to “get-preview-of-edited-symptom.php” PHP script, this script collects the grading settings data of the symptom from the database and according to its grading settings prepares the different versions of the symptom (i.e. original version, converted version, etc.) using the “convertTheSymptom()” function which is available in the “functions.php” PHP page. And sends populated preview result data back, which gets displayed to the user.

After that when user clicks the Submit button in the symptom edit popup, by clicking the submit button we POST the form data to “edit-original-or-converted-symptom.php” PHP script, In this script we are updating the edited symptom string in the database tables – “quelle_import_test” and other applicable dynamic comparison table. Here we are also setting the individual grading setting for the symptom in the symptom_grading_settings table.

**CE or SWAP CE:**

When we click on the CE or SWAP CE button, we show or populate the symptom data in the CE or SWAP CE popup by fetching from the data fields or hidden fields of that symptom in the HTML. Also we fetch symptom grading data from the database using “fetch-symptom-settings-information.php” script in “connect-edit-exp.js”.

When we click on the Preview button on the CE or SWAP CE popup, we POST the popup from data to “get-preview-of-connect-edited-symptom.php” PHP script through “connect-edit-exp.js” JavaScript page using AJAX. On the basic of the submitted data  “get-preview-of-connect-edited-symptom.php”  PHP script prepare the preview result and sends it back to the page. This PHP script collects the grading settings of the symptom and according to its grading settings prepares the different versions of the symptom (i.e. original version, converted version, etc.) using the “convertTheSymptom()” function which is available in the functions.php PHP page.

When we finally Submit the CE or SWAP CE process, by clicking the submit button we POST the form data to “connect-edit-operation.php” PHP script, Here in this PHP script we store the connect information in database in the dynamic connection table of that comparison (i.e. comparison_table_34_2_257_de_connections). And we also store the individual grading setting data with the comparison ID in the database table “symptom_grading_settings” . Here comparison ID is stored in the “pre_comp_id” (by default it’s value is 0) column of the DB table “symptom_grading_settings”.

```
Related scripts:

dev-exp/functions.php

dev-exp/symptoms.php

dev-exp/get-editable-symptoms.php

dev-exp/get-preview-of-edited-symptom.php

dev-exp/edit-original-or-converted-symptom.php

dev-exp/fetch-symptom-settings-information.php

dev-exp/connect-edit-exp.js

dev-exp/get-preview-of-connect-edited-symptom.php

dev-exp/connect-edit-operation.php
```