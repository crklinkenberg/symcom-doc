---
{"dg-publish":true,"permalink":"/topics/new-modification-in-ce-swap-ce-concept/"}
---


According to our new modifications now if a symptom has two CE connection (through multiple level comparison)

Now if we remove or disconnect one of the connections the initial symptom will go back to its previous state. Which means if we disconnect the last or we can say the latest CE connection then the initial symptom will go back to its second last CE connection state.

Similarly, if we disconnect the second last CE connection only, then the initial will remain same, because the last CE connection is still there, So the initial symptom still holds the effect of the last CE connection.

In short, an initial symptom which has connections will always be displayed with the effect of its last or we can say the latest connection.

**What happens with disconnected symptom?:**

If the disconnected symptom belongs to initial source(s) then it will appear as an initial symptom somewhere in the comparison.

And if the disconnected symptom belongs to comparative source(s) then it will appear as a comparative symptom in the comparison in its appropriate place(s).

Example:

Suppose we are comparing A_B_C with D_E_F. Here A_B_C is initial source and D_E_F is comparing source.

Here A_B_C source can have any kind of earlier connection (i. e. C, CE, SWAP CE, P, etc.). Now if we disconnect any earlier connection of A_B_C the disconnected symptoms will appear as initial symptom.

Same goes for D_E_F (which is the comparative source) here if we disconnect any earlier connection of D_E_F, the disconnected symptom will appear as comparative symptom.

**Concept of grading related to connection process:**

In each comparison when we do a connection where there is an option available to do grading changes for that particular symptom through this connection, this individual grading data of that particular symptom is getting stored separately on each connection basics or we can say on each comparison basics.

A symptom can get its gradings or grading data from its source where it belongs.

Or

A symptom can have its individual grading data of itself.

If required a user can set individual gradings for a particular symptom by using the symptom edit process.

A User also has the facility to set grading for a symptom in a few connections process (i.e. CE, SWAP CE, etc.)

By default, the source’s grading setting (If available) gets applied on all the symptoms of that source.

But if a symptom has its own individual grading setting, which that symptom can get through symptom edit process or through a connection process (i.e. CE, SWAP CE, etc.), then that symptom always follows its individual grading setting.

**Grading related to disconnection:**

When a user disconnects a connection (i.e. CE, SWAP CE, etc.) where the disconnecting symptom has individual grading which got obtained through that connection.

In this disconnection process that individual grading also gets deleted, which got obtained through that connection.

**Technical Workflow:**

When we click on the CE or SWAP CE button, we show or populate the symptom data in the CE or SWAP CE popup by fetching from the data fields or hidden fields of that symptom in the HTML. Also we fetch symptom grading data from the database using “fetch-symptom-settings-information.php” script in “connect-edit-exp.js”.

When we click on the Preview button on the CE or SWAP CE popup, we POST the popup from data to “get-preview-of-connect-edited-symptom.php” PHP script through “connect-edit-exp.js” JavaScript page using AJAX. On the basic of the submitted data  “get-preview-of-connect-edited-symptom.php”  PHP script prepare the preview result and sends it back to the page. This PHP script collects the grading settings of the symptom and according to its grading settings prepares the different versions of the symptom (i.e. original version, converted version, etc.) using the “convertTheSymptom()” function which is available in the functions.php PHP page.

When we finally Submit the CE or SWAP CE process, by clicking the submit button we POST the form data to “connect-edit-operation.php” PHP script, Here in this PHP script we store the connect information in database in the dynamic connection table of that comparison (i.e. comparison_table_34_2_257_de_connections). And we also store the individual grading setting data with the comparison ID in the database table “symptom_grading_settings” . Here comparison ID is stored in the “pre_comp_id” (by default it’s value is 0) column of the DB table “symptom_grading_settings”.   

When we click on the disconnection button of CE or SWAP CE connection, it again takes the POST data to the “connect-edit-operation.php” PHP script, here we delete the connection from the dynamic connection table of that comparison. We are also deleting the individual grading setting of the CE or SWAP CE symptom with the help of comparison ID or we can say with the help of the “pre_comp_id” column of the table “symptom_grading_settings” we also delete the individual grading setting of that CE or SWAP CE connection. Then we fetch the last available connection of the symptom (if available after the current disconnection) from the dynamic connection table of the comparison and then updates the symptom to its last available connection’s state.

Related scripts:

dev-exp/functions.php

dev-exp/fetch-symptom-settings-information.php

dev-exp/connect-edit-exp.js

dev-exp/get-preview-of-connect-edited-symptom.php

dev-exp/connect-edit-operation.php