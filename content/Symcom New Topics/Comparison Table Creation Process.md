Associated files location: `symcom-core-app/dev-exp/comparison`

When comparison button is clicked, the form with id "symptom_comparison_form" is submitted and an ajax request is sent to `check-if-comparison-table-exist.php` script along with all the relevant data required to start the comparison.

Below link shows the workflow of all the scripts involved in the process:

[Digramatical illustration of the comparison process.](https://app.eraser.io/workspace/GRQZN2ItG5mVk66JIday?origin=share)

Workflow of `check-if-comparison-table-exist.php` script:
```
NOTE:
The initial and comparing sources are individual sources present in the sources table.
These sources are created in below steps:
1. Adding a book/magazine via master data section. 
2. This book is selected in combination with medicine in the import page.
3. The symptoms from docx file is copied and pasted and after import is done, it is considered as source (S).
4. The setting of the import is kept in import_source_settings SQL table.
5. The books/magazine are kept in sources SQL table.
6. The medicine and authors are kept in separate SQL table.
7. When any of the sources S, is involved in comparison, these two are compared and when comparison is finazlied both sources are combined i.e. the symptoms of each of these source is combined and a new source is created for the medicine involved in the comparison.
8. In case the comparison is deleted, then the sources involved in comparison are activated again and displayed in the materia medica page.
```

1. The comparison table name is created using the word "comparison_table_" before medicine id, initial source id, comparing source id and the comparison language.
2. Comparison settings is stored in PHP session.
3. The table is checked in SQL `comparison_settings` table. If the table is present, then it is directly loaded with the comparison settings.
4. If it is not present then dynamic comparison table creation process starts.
5. The new comparison is stored as a new source in `sources` SQL table. As when the comparison is completed and finalized, it will be considered as a new source.
6. The `import_source_settings` is accordingly maintained with all associations.
7. The `rel_source_medicine` table is also inserted with the new relationships.
8. Since sources involved in comparisons are not shown in `materia medica` web-page therefore, `is_materia_medica` value for each of the sources involved in the comparison is set to 0.
9. Then the setting of the comparison is saved in `comparison_settings` SQL table.
10. The comparison and highest matches tables are created with queries.
11. The total initials which will be involved in the comparison is calculated.
12. Call to `create-dynamic-comparison-table.php` script is made via `shell_exec()`. As the comparison process should run even when the website is closed, so commands are run in bash functions.
13. All parameters sent to the script is escaped using `escapeshellarg()`. It is in this script that insertion of initial symptoms and the comparing symptoms takes place  eventually, after which the `comparison_settings` SQL table is updated with status `done` to mark the comparison as successful.

```
Parameters sent to create-dynamic-comparison-table.php` are:

comparisonTable => comparison table name.

savedinitialSourceTable => comparison table name when initial source is a saved comparison.

savedDataConnectionsTableOfInitialSource => connection table name when initial source is a saved comparison.

initialSourceId => initial source id which is quelle_id.

medicineId => medicine id.

comparingSourceIds => comparing source ids.

preComparisonMasterDatainsertedId => id from pre comparison master table.

initialRowsTotalRowsQueryRows => total number of initial source rows.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.

clientIPToSent => The client IP.

sessionUserIdToSent => the user ID or editor Id.

absoluteUrlToSent => absolute url which is later used in the automatic connection process.

fileExecutionLocation => The file execution location for bash commands.
```

Workflow for `create-dynamic-comparison-table.php` script:

1. The parameters sent using shell_exec in the previous script is received.
2. On the basis of `intialRowsTotalRowsQuery` value, total batches are computed. Batch Size can be controlled from `batchSize` PHP variable.
3. Each batch is iterated using a for loop and in each loop shell_exec() command is executed to `create-dynamic-initial-insertion-restart.php` script.
4. The initial symptoms are send in batches to `create-dynamic-initial-insertion-restart.php` script. It is in this script that the comparing symptoms for each of the initial symptoms are selected in new batches, first it is inserted in comparison_temp table, and then it is inserted into the main comparison SQL table.
5. Once all insertions of the comparing symptoms and initial symptoms are done, connections table is created. A temporary connections table `temp_comparison_table_connections` is created and then automatic connection of symptoms is executed.
6. Once the script finishes all the above steps, the `comparison_settings` SQL table is updated with status `done` to mark the end of the comparison.
```
Parameters sent to "create-dynamic-initial-insertion-restart.php" script are:

comparisonTable => comparison table name.

savedinitialSourceTable => comparison table name when initial source is a saved comparison.

savedDataConnectionsTableOfInitialSource => connection table name when initial source is a saved comparison.

initialSourceId => initial source id which is quelle_id.

medicineId => medicine id.

comparingSourceIds => comparing source ids.

preComparisonMasterDatainsertedId => id from pre comparison master table.

startLimitOfInitialsToSent => start limit for mysql query.

endLimitOfInitialsToSent => end limit for mysql query.

savedComparisonConnectionsArrToSent => array which includes connections table if sources are already saved combined sources.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.
```


Workflow for `create-dynamic-initial-insertion-restart.php` script:

1. The parameters sent by its parent script through script is received.
2. Based on the `startLimitOfInitials` and `endLimitOfInitials` limit values, the initial symptoms are fetched out.
3. For each of these initial symptoms, a `shell_exec()` command is executed for `create-dynamic-comparing-selection-restart.php` script.

```
Parameters sent to create-dynamic-comparing-selection-restart.php script are:

savedComparingSourceTableToSent => comparison table name when comparing is already saved combined source.

comVal => quelle id of the comparing source.

comparisonTableToSent => comparison table name.

runningInitialSymptomIdToSent => initial id of the current loop.

medicineId => medicine id.

startLimitOfComparingToSent => start limit for mysql query.

endLimitOfComparingToSent => end limit for mysql query.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.
```

4. After successful execution of each loops, this script searches for the temporary table where comparing symptoms data are kept by the `create-dynamic-comparing-selection-restart.php` script.
5. When temporary table exists and no error is found the comparing symptoms located in the temporary table are inserted to the dynmic table batch by batch.
6. Batch size can be assigned with `comparingInsertionBatchSize` PHP variable.
7. For each batch `shell_exec()` command is executed for `create-dynamic-comparing-insertion-restart.php` script which does the insertion in the comparison table.

```
Parameters sent to "create-dynamic-comparing-insertion-restart.php" script are:

comparisonTableToSentInsertion => comparison table name.

startLimitOfComparingInsertionToSent => start limit for mysql query.

endLimitOfComparingInsertionToSent => end limit for mysql query.
```

Workflow for `create-dynamic-comparing-selection-restart.php` script:

1. Parameters sent from parent script `create-dynamic-initial-insertion-restart.php` are received.
2. Checks if temporary table is created for this comparison. If not exist then temporary table is created.
3. Comparing symptoms are fetched and inserted in the temporary tables.
  

Workflow for `create-dynamic-comparing-insertion-restart.php` script:

1. Parameters sent from parent script `create-dynamic-initial-insertion-restart.php` are received.
2. Comparing symptoms are fetched from temporary tables using `startLimitOfComparingInsertion` and `endLimitOfComparingInsertion` values.
3. The comparing symptoms fetched are finally inserted into comparison table.


Basic row insertion illustration:

Below states the flow of execution for 3000 comparing of symptoms. Let's say we have 100 initial symptoms and in each batch 10 initial symptoms are sent for execution,  each of the  initial symptom is compared with 3000 comparing symptoms. And these 3000 comapring symptoms are first selected and inserted in temporary table in batches of 1000 untill all 3000 comparing symptoms are reached. Then from the temporary table out of the 3000 comparing symptoms which are freshly inserted, comparing symptoms are selected in batches of 500 and inserted in dynamic comparison table.

  
### Insertion for only one initial symptom is shown here.

```
For 10 intial symptoms per batch:

Assuming overall 3000 comparing symptoms:

    1st intial symptom:

    {

        1000 comparing symptoms are selected and compared.

            -> 1000 comparing symptoms are inserted in temp table.

        next 1000 comparing symptoms are selected and compared.

            -> next 1000 comparing symptoms are inserted in temp table.

        next 1000 comparing symptoms are selected and compared.    

            -> next 1000 comparing symptoms are inserted in temp table.

    },

    {

        500 comparing symptoms are selected from temp table and inserted to comparison table.

        next 500 comparing symptoms are selected from temp table and inserted to comparison table.

        .

        .

        until 3000 all comparing symptoms are reached

    }

    temporary table is truncated here.   

    2nd initial symptom:

    {

        .

        .

    }

    3rd initial symptom:

    .

    .

    10th initial symptom:
```

### Controlling Batch Size & Performance:

```
1. Number of initial symptoms sent for execution is controlled by "batchSize" PHP variable in "create-dynamic-comparison-table-batch-processing.php" script.

  

2. Number of comparing symptoms to be compared for a particular initial is contorlled by "comparingBatchSize" PHP variable in "create-dynamic-comparing-insertion-restart.php" script.

  

3. Number of comparing symptoms to be inserted in the comaprison table is controlled by "comparingInsertionBatchSize" PHP variable in "create-dynamic-comparing-insertion-restart.php" script.
```


Important Configuration Setting:

1. Persistent database connection is used in all the scripts. In order to achieve it `db-connection-pool.php` script is used, which keeps the connection to the separate scripts intact.
2. `memory_limit` in PHP is kept infinite with the help of `ini_set()` PHP function.
3. `max_execution_time` is set to 0 with the help of `ini_set()` PHP function.
4. `max_input_vars` is set to 10000 with the help of `ini_set()` PHP function.
5. Customized error catching is done in a separate file. Location `dev-exp/dynamic-error-logs/error.log`. Please give permission to the file from the server to execute flawlessly.
6. MySQL variables like `interactive_timeout`, `wait_timeout` and `connect_timeout` are all default values at present.
7. 16 GB and 4 cores for best results.

  

NOTE:  If more number of initial or comparing symptoms are compared, please ensure to tune the `batchSize`, `comparingBatchSize` and `comparingInsertionBatchSize` PHP variables for efficient system performance. For larger number of initials or comparing symptoms these values should be lower than the existing values for this particular server configuration.

  
## Advantages and optimization as compared to previous code:

1. The previous workflow executes the whole process in one script due to which the resources allocated by memory are not released due to which full memory was utilized by the process. New process executes each part of symptom selection and insertion in separate scripts, these scripts after execution clears the resources allocated to them and thereby only 50% of the memory was used by the process, other 50% was cached by the system to perform all operations efficiently.
2. Due to batch processing in new approach, the batch size can be manipulated as needed, resulting control of memory even for large data set comparison.
3. As compared to previous approach, new approach is 25% more faster in terms of overall process completion.
  

### Additional Experiences & Important Notes:

1. Most PHP variables used are voluntarily unset after each operation as this helps in clearing the memory allocated more frequently, thereby these processes are not completely dependent on PHP garbage collector for resource operations.
    
2. All PHP variables and arrays are carefully checked and proceeded for operation in each script as undefined variables leads to PHP warnings and notices and this leads to creation of a large log file.
    
3. The whole set up is isolated from the existing development, staging and production environment for tests as there are many functions and scripts dependent on these processes and change of any used script during on going operation leads to error.
    
4. PHP error logs are also generated by a custom script `create-dynamic-error-catch.php` which saves the errors in custom file inside the comparison-writing directory inside `dev-exp`. This needs to be removed later when full integration is done.
    
5. For database connection, a temporary static PHP script `db-connection-pool.php` is used at present. This  also needs to be dynamic later when full integration is done.
    
6. Persistent database connection is used in the process. This ensures that no new connections for database are created for MySQL operations resulting in a uniform and stable MySQL processes throughout the operation.
    
7. Exception handling for `shell_exec()` command using `error_get_last()` does not confirm accuracy in all cases so it is being used carefully.
    
8. Due to batch processing, memory consumption by both PHP and MySQL is uniform and hovers around 7 GB of used memory. CPU processing stays stable at 20%.
    
9. Please ensure not to run large comparison parallel with resource intensive operations like running another large comparison or git push from different environment during large comparison operation as this may crash the server.
    

  

## General technique for comparison estimation:

```
Let's say if:

    Number of initial symptoms (A) = 4109

    Number of comparing symptoms (B) = 3439

  

    Total expected rows in dynamic comparison mysql table = A * B + A

    which will be = (4109 * 3439) + 4109

                  = 1,41,34,960 rows.

  

    With configuration of 16Gb memory and 4 core CPU:

    Total operation time : 14 hours.

    Total space consumed by comaprison mysql table: 18.1 Gb.
```