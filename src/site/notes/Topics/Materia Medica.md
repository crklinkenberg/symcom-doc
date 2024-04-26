---
{"dg-publish":true,"permalink":"/topics/materia-medica/"}
---


Contains all the source information. Provide with a panel for custom search operation.

Technical Details:

The search panel parameters are send with “POST” method.

Name used in the html form for searching: arznei_search_medica.

Joining of SQL tables is for the result search.

Tables used: quelle_import_master, quelle, pre_comparison_master_data.

The field “is_materia_medica” in “quelle” SQL table should be “1”.

  

Comparison History:

History of comparison of source is present here. Page provided with a search panel for custom search.

Whenever a comparison is saved by the supervisor, a copy of the latest comparison (with all connections) is saved in the history page. After a comparison is saved, it is then converted to a final state which becomes eligible for further comparisons. By going to the history page the supervisor can again reactivate the last states of the comparisons of that source in case any more repair is required. Reactivating makes the source comparable again.

Technical Details:

SQL tables used: quelle_import_master, quelle, quelle_autor, autor, pre_comparison_master_data, pre_comparison_master_data_for_history

  

  

 Saving of a comparison in the history page from the supervisor:

 Whenever a comparison is saved by the supervisor, the quelle_id, arznei_id and comparison_name is fetched from the “pre_comparison_master_data” table of that particular comparison, it is then send via an API to “update-comparison-name-new.php” script for further operations.

  

Workflow of this script:

- Fetches all information of that source from the “pre_comparison_master_data” SQL table.
    
- Inserts all the fetched records in the “pre_comparison_master_data_for_history” SQL table.
    
- The inserted id is then kept in a PHP variable.
    
- Dynamic creation of history table name is done for storing the state of the comparison.
    
- Dynamic name created is used to create new history tables: dyanamic table, connections, completed and highest_matches.
    

Reactivation from the history table is done using the “reactivate-a-comparison-history.php” script in the “history.php” page. When reactivation is done the “comparison_save_status” value is updated to “1” in the “pre_comparison_mster_data” SQL table, which makes the comparison compatible for comparing again by the editors.