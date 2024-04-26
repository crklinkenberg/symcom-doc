When a comparison is saved, the HTML class “comparison-table-save-btn” is revoked. A pop up is displayed to confirm the editor’s input and then the program checks for unmarked initial symptoms or non secure connections with the help of “check-unmarked-symptoms.php” script via an ajax call. If any unmarked or non secure connections are found then the editor is notified with a pop up and then redirects the editor to the secure the connections for saving the comparison.

If no unmarked or non secure connections are found then the save process is followed by the “savingComparison()” js function. This function submits the form with id “saveSubmit” and redirects to the main comparison page with HTTP method “POST”.

“savingComparison(param)” takes parameters 1 or 0.

This function changes the input value of the “temp_unmark_check” id as per the param value. For saving the comparison the value of param = 0.

The form with id “saveSubmit” takes input three input values : save_comparison, similarity_rate_save and temp_unmark_check and is submitted with the help of HTTP POST method.

Saving steps in PHP script:

- The form input values are detected.
    
    If “temp_unmark_check” value = 1 then unmarked symptoms are listed in the comparison page.
    
    If “temp_unmark_check” value = 0, then save process follows.
    
- For editor:
    

	- The “comparison_save_status” SQL field of tables “pre_comparison_master_data” and “quelle” is updated to “1”. The comparison status in materia-medica page is now shown in “yellow” color.
    

- For supervisor:
    

	- Total unmarked initial symptoms with no comparatives match are taken out in an array with the help of “unmarkedSymptoms()” function.
	    
	- All symptoms are then sorted according to their source year and taken out in an array `$savedSortedIdsArray[]` with the help of “rearrangeSymptomsInOrder()” function.
	    
	- Completed table with comparison table name and suffix “_completed” of the comparison is created.
	    
	- The “quelle_id” of that particular is taken out from the “pre_comparison_master_data” table. This “quelle_id” forms new “quelle_id” for that saved source.
	    
	- Each id from the `$savedSortedIdsArray[]` is iterated and information is fetched out from the comparison table. This information is then inserted into the completed table.
	    
	- After complete insertion, symptoms with paste edit, connect-edit, swap connect, swap connect-edit connections are modified and latest symptom text and associated values are updated in the completed table.
    

The “comparison_save_status” SQL field of tables “pre_comparison_master_data” and “quelle” is updated to “2”. The comparison status in materia-medica page is now shown in “green” color and the comparison is finally saved and is ready for more further comparisons.