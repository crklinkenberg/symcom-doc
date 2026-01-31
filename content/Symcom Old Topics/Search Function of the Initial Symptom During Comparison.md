---
{"dg-publish":true,"permalink":"/topics/search-function-of-the-initial-symptom-during-comparison/"}
---

#comparison 

### Technical Details:
JavaScript Data Tables are used for this function.

Table is generated dynamically from the search input and is appended to the search modal in the frontend.

Table is defined on the `dataTablesConfig.js` script using the HTML id `search_initial_table`.

For fetching symptom information HTML id `search_initial_table` and class `tbody` along with JavaScript event `click` is used.
  
Fetching of info is exactly same as the other info fetching function present under "Info & Linkage" column in the comparison process.

NOTE: Any change in the other info fetching function needs to be modified here too.

On change of the radio switch from the pop up, the table HTML elements are controlled using jQuery. `btn-initial` and `btn-comparative` classes controls this.

`search_initial_table_all` id is used for the search result from initial.

`search_initial_table` id is used for search result from comparing.

`searchFunctionData(parentRowId, comparison_table_name, comparison_language, search_only_initials, callback)` JS function fetches the information from the database. This function uses `get-symptom-search-result-modified.php` script in accordance with ajax to fetch and display the result in data tables.

`search_only_initials` parameter in this function is the flag and when true this fetches only the initial symptoms from the database.

```
Related scripts:
1. dataTablesConfig.js
2. custom.css
3. comparison-table-page-modules.php
4. get-symptom-search-result-modified.php
```


### Multiple word searching
The search function has been updated with multiple word search. For this the default `datatable` classes `dataTables_filter` are modified with new HTML id `search-comparing-input-field` and `search-initial-input-field` to control the search input field of the `datatables`.

`keyup` events are added to both the above mentioned ID's and highlighting of the new search results have been added to both of these events. 

NOTE: Search icon is added to the comparative symptom in all the comparison.