---
{"dg-publish":true,"permalink":"/topics/search-function-of-the-initial-symptom-during-comparison/"}
---


Technical Details:

  

JavaScript Data Tables are used for this function.

  

Table is generated dynamically from the search input and is appended to the seach modal in the frontend.

  

Table is defined on the "dataTablesConfig.js" script using the HTML id "search_initial_table".

  

For fetching symptom information HTML id "search_initial_table" and class "tbody" along with JavaAcripts event "click" is used.

  

Fetching of info is exactly same as the other info fetching function present under "Info & Linkage" column in the comparison process.

  

NOTE: Any change in the other info fetching function needs to be modified here too.

  

On change of the radio switch from the pop up, the table HTML elements are controlled using jQuery. "btn-initial" and "btn-comparative" classes controls this.

  

"search_initial_table_all" id is used for the search result from initial.

"search_initial_table" id is used for search result from comparing.

  

searchFunctionData(parentRowId, comparison_table_name, comparison_language, search_only_initials, callback) js function fetches the information from the database. This function uses "get-symptom-search-result-modified.php" script in accordance with ajax to fetch and display the result in data tables.

  

"search_only_initials" parameter in this function is the flag and when true this fetches only the intial symptoms from the database.

  

Related scripts:

1. dataTablesConfig.js

2. custom.css

3. comparison-table-page-modules.php

4. get-symptom-search-result-modified.php