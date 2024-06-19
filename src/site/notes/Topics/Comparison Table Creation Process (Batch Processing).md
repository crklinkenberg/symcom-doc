---
{"dg-publish":true,"permalink":"/topics/comparison-table-creation-process-batch-processing/"}
---

Please Note: This process is not yet integrated to Symcom. Only tested. New codes from `create-dynamic-comparison-table.php` script might not be updated in this process. These needs review and updates before integration.

When comparison button is clicked, the form with id "symptom_comparison_form" is submitted and an ajax request is sent to "check-if-comparison-table-exist-new.php" script along with all the relevant data required to start the comparison.

Below link shows the workflow of all the scripts involed in the process:

[Digramatical illustration of the comparison process.](https://app.eraser.io/workspace/GRQZN2ItG5mVk66JIday?origin=share)

Workflow of check-if-comparison-table-exist-new.php script:

- The comparison table name is created using the word "comparison_table_" before arznei id, initial source id, comparing source id and the comparison language.
    
- The existing table is first searched in the system from the "pre_comparison_master_data" mysql table and if the table is not present all prerequisite operations are done and comparison table and its highest matches table is created.
    
- The number of initial symptoms is calculated and is then sent as parameters in the shell_exec() command to the script "create-dynamic-comparison-table-new.php".
```
Parameters sent are:

comparisonTable => comparison table name.

savedinitialSourceTable => comparison table name when initial source is a saved comparison.

savedDataConnectionsTableOfInitialSource => connection table name when initial source is a saved comparison.

initialSourceId => initial source id which is quelle_id.

arzneiId => medicine id.

comparingSourceIds => comparing source ids.

preComparisonMasterDatainsertedId => id from pre comparison master table.

initialRowsTotalRowsQueryRows => total number of initial source rows.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.
```

Workflow for create-dynamic-comparison-table-batch-processing.php script:

- The parameters sent using shell_exec in the previous script is received.
    
- On the basis of initialRowsTotalRowsQuery value, total batches are computed. Batch Size can be controlled from "batchSize" PHP variable.
    
- Each batch is iterated using a for loop and in each loop shell_exec() command is executed to "create-dynamic-initial-insertion-restart.php" script.
```
Parameters sent to "create-dynamic-initial-insertion-restart.php" script are:

comparisonTable => comparison table name.

savedinitialSourceTable => comparison table name when initial source is a saved comparison.

savedDataConnectionsTableOfInitialSource => connection table name when initial source is a saved comparison.

initialSourceId => initial source id which is quelle_id.

arzneiId => medicine id.

comparingSourceIds => comparing source ids.

preComparisonMasterDatainsertedId => id from pre comparison master table.

startLimitOfInitialsToSent => start limit for mysql query.

endLimitOfInitialsToSent => end limit for mysql query.

savedComparisonConnectionsArrToSent => array which includes connections table if sources are already saved combined sources.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.
```

- Upon completion of the above for loop another shell_exec() command are executed. On for "create-dynamic-insertion-highest-matches.php" and another for "create-dynamic-final-closure.php" script. The first one inserts the highest matched value of each comapring symptoms in the highest matches table. The second one inserts connections of each intial and comparing source if they combined saved source.

Workflow for create-dynamic-initial-insertion-restart.php script:

- The parameters sent by its parent script thrrough script is received.
    
- Based on the "startLimitOfInitials" and "endLimitOfInitials" limit values, the initial symptoms are fetched out.
    
- For each of these intial symptoms, a shell_exec() command is executed for "create-dynamic-comparing-selection-restart.php" script.

```
Parameters sent to create-dynamic-comparing-selection-restart.php script are:

savedComparingSourceTableToSent => comparison table name when comparing is already saved combined source.

comVal => quelle id of the comparing source.

comparisonTableToSent => comparison table name.

runningInitialSymptomIdToSent => initial id of the current loop.

arzneiId => medicine id.

startLimitOfComparingToSent => start limit for mysql query.

endLimitOfComparingToSent => end limit for mysql query.

comparisonOptionToSent => comparison option.

comparisonLanguageToSent => comaprison language.
```

- After successful execution of each loops, this script seaches for the temporary table where comparing symptoms data are kept by the "create-dynamic-comparing-selection-restart.php" script.
    
- When temporary table exists and no error is found the comparing symptoms located in the temporary table are inserted to the dynmaic table batch by batch.
    
- Batch size can be assigned with "comparingInsertionBatchSize" PHP variable.
    
- For each batch shell_exec() command is executed for "create-dynamic-comparing-insertion-restart.php" script which does the insertion in the comparison table.

```
Parameters sent to "create-dynamic-comparing-insertion-restart.php" script are:

comparisonTableToSentInsertion => comparison table name.

startLimitOfComparingInsertionToSent => start limit for mysql query.

endLimitOfComparingInsertionToSent => end limit for mysql query.
```

Workflow for "create-dynamic-comparing-selection-restart.php" script:

1. Parameters sent from parent script "create-dynamic-initial-insertion-restart.php" are received.
    
2. Checks if temporary table is created for this comparison. If not exist then temporary table is created.
    
3. Comaparing symptoms are fetched and inserted in the temporary tables.
    

  

Workflow for "create-dynamic-comparing-insertion-restart.php" script:

1. Parameters sent from parent script "create-dynamic-initial-insertion-restart.php" are received.
    
2. Comapring symptoms are fetched from temprary tables using "startLimitOfComparingInsertion" and "endLimitOfComparingInsertion" values.
    
3. The comaparing symptoms fetched are finally inserted into comparison table.
    

  

Workflow for "create-dynamic-final-closure.php" script:

1. Connection table is created and connections if anything is found is inserted.
    
2. Pre comparison master data table is updated and status field is set to "done".
    

  

Important:

In execution of this whole process, the initial symptom synonyms are kept in a txt file under the directory "comparison-writing". After the whole process gets executed, this txt file is deleted from the directory.

  

Basic row insertion illustration:

Below states the flow of execution for 3000 comparingf symptoms. Let's say we have 100 initial symptoms and in each batch 10 initial symptoms are sent for execution,  each on of the  initial symptom is compared with 3000 comparing symptoms. And these 3000 comapring symptoms are first selected and inserted in temporary table in batches of 1000 untill all 3000 comparing symptoms are reached. Then from the temporary table out of the 3000 comparing symptoms which are freshly inserted, comparing symptoms are selected in batches of 500 and inserted in dynamic comparison table.

  

Insertion for only one initial symptom is shown here.
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

Controlling Batch Size & Performance:
```
1. Number of initial symptoms sent for execution is controlled by "batchSize" PHP variable in "create-dynamic-comparison-table-batch-processing.php" script.

  

2. Number of comparing symptoms to be compared for a particular initial is contorlled by "comparingBatchSize" PHP variable in "create-dynamic-comparing-insertion-restart.php" script.

  

3. Number of comparing symptoms to be inserted in the comaprison table is controlled by "comparingInsertionBatchSize" PHP variable in "create-dynamic-comparing-insertion-restart.php" script.
```


Important Configuration Setting:

1. Persistent database connection is used in all the scripts.
    
2. memory_limit in PHP is kept infinite with the help of ini_set() php function.
    
3. max_execution_time is set to 0 with the help of ini_set() php function.
    
4. max_input_vars is set to 10000 with the help of ini_set() php function.
    
5. Customized error catching is done in a separate file.
    
6. Mysql variables like interactive_timeout, wait_timeout and connect_timeout are all default values at present.
    
7. 16gb and 4 cores.
    

  

NOTE:  If more number of initial or comapring symptoms are compared, please ensure to tune the "batchSize", "comparingBatchSize" and "comparingInsertionBatchSize" PHP variables for efficient system performance. For larger number of intials or comapring symptoms these values should be lower than the existing values for this particular server configuration.

  

Advantages and optimization as compared to previous code:

1. The previous workflow executes the whole process in one script due to which the resources allocated by memory are not released due to which full memory was utilized by the process. New process executes each part of symptom selection and insertion in separate scripts, these scripts after execution clears the resources allocated to them and thereby only 50% of the memory was used by the process, other 50% was cached by the system to perform all operations efficiently.
    
2. Due to batch processing in new approach, the batch size can be manipulated as needed, resulting control of memory even for large data set comparison.
    
3. As compared to previous appraoch, new appraoch is 25% more faster in terms of overall process completion.
    

  

Additional Experiences & Important Notes:

1. Most PHP variables used are voluntarily unset after each operation as this helps in clearing the memory allocated more frequently, thereby these processes are not completley dependant on PHP garbage collector for resource operations.
    
2. All PHP variables and arrays are carefully checked and proceeded for operation in each script as undefined variables leads to PHP warnings and notices and this leads to creation of a large log file.
    
3. The whole set up is isolated from the existing development, staging and production environment for tests as there are many functions and scripts dependant on these processes and change of any used script during on going operation leads to error.
    
4. PHP error logs are also generated by a custom script "create-dynamic-error-catch.php" which saves the errors in custom file inside the comparison-writing directory inside dev-exp. This needs to be removed later when full integration is done.
    
5. For database connection, a temporary static php script "db-connection-pool.php" is used at present. This  also needs to be dynamic later when full integration is done.
    
6. Persisent database connection is used in the process. This ensures that no new connections for database are created for mysql operations resulting in a uniform and stable mysql processes throughout the operation.
    
7. Exception handling for shell_exec() command using "error_get_last()" does not confirm accuracy in all cases so it is being used carefully.
    
8. Due to batch processing, memory consumption by both php and mysql is uniform and hovers around 7GBs of used memeory. CPU processing stays stable at 20%.
    
9. Please ensure not to run large comaprison parallely with resource intensive operations like running another large comaprison or git push from different environment during large comparison operation as this may crash the server.
    

  

General technique for comaprison estimation:
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