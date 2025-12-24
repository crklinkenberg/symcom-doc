---
{"dg-publish":true,"permalink":"/topics/marking-of-symptoms-technical-details/"}
---

#comparison 

Database: In the main comparison SQL table, the marking is kept in a field name “marked”. The value is “1” when marking is active and by default, the value is “0”.

Automatic marking functionality by the program:

- Initial symptoms with marked value “0” is kept in a php array “markSymptomIds[]”.
    
- This array is then transferred to js array with array name “markSymptomIdsFinalArray[]”.
    
- All the ids in this array are then iterated and if there are no comparatives below this initial, a check mark is given using js function. The general non secure icon is also disabled at this point.
    

Note: Automatic check marks given by the program is dynamic and the checkmarks will change its behavior according to the cut-off percentage of the comparison. Check marks are not directly updated in the SQL table, only when comparison is saved with supervisor privilege the marking with no comparatives will be given a value “1” and during the full comparison saving process.

  

  

Manual marking by the user:

When marking is given manually, operation is proceed with the help of ajax.

"update-marking-symptoms.php" page is used. The marked field in SQL table is updated to “1”.

  

  

General Non Secure (Technical Details):

General non secure icon is disabled for initial symptoms if the initial has connections or if there are no comparatives below the initial.

Class ”gen-ns” is used for operating symptoms with general non secure.

Fetching information:

Initial id and the comparison table name is sent as parameters to “get-general-non-secure-info-comparison-table.php” to fetch any general non secure information of the initial symptom.

  

addGenNscNote function:

Js function “addGenNscNote(param)” is used for adding or modifying information related to general non secure. For enabling general non secure, param value is “1” and for disabling, the value is “0”.

Value for “confirming” is stored in “ns_confirm” and value for “new” is stored in “ns_new”.

Parameters are then to “update-symptom-info-comparison-table.php” via ajax where further backend modification with SQL table is done.

NOTE:

PHP flag “editingNs” is used to check the editing mode for operation of non secure symptoms. Accordingly “data-mark” attribute value is changed with element id “checkingNS”.

  

Non secure connect and paste (Technical Details):

Fetching of information:

Class “symptom-soft-connect-btn” and “symptom-soft-paste-btn” is used for opening the pop up and fetching information from the database.

“get-non-secure-info-comparison-table.php” script is used to fetch information from the database.

Backend modification:

Js function “addnscNote()” is used for connect and “addnscNotePaste()” is used for paste non secure connections.

Some important PHP functions:

- checkInitialInConnectionForConnectConfirm(database, comparisonTable, initialId):
    
    This function checks if the initial symptom has more than one connect connection in the connection table. The return value is used for further updation the “non_secure_connect” value in the comparison table during modification of the non secure connect connection.
    
- checkInitialInConnectionForPasteConfirm (database, comparisonTable, initialId):
    
    This function checks if the initial symptom has more than one paste connection in the connection table. The return value is used for further updation the “non_secure_paste” value in the comparison table during modification of the non secure paste connection.
    
- checkComparativeConnection(database, comparisonTable, initialId):
    
    Checks for more than one connection with the same initial in the connection table.
    
- `initialCustomListing($param, $db, $comparison_table, $page_start, $per_page_initial)`:
    
    This function helps in initial symptom listing in the comparison page. As per page number the query is modified.