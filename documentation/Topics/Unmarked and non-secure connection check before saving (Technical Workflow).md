PHP script “check-unmarked-symptoms.php” is associated with this task.

- Initial id’s having ongoing connections are taken in a PHP variable `$totalUnmarkedNoComparatives` with the help of “unmarkedSymptoms()” array.
    
- All unmarked initial ids are then taken out. And the subtracted value from the `$totalUnmarkedNoComparatives` is then returned to the user which is shown in the pop up.
    

	This script also counts the non secure connections and returns its value to the user. From the comparison table, below sql table fields are searched for retrieving the total non secure symptoms:

  

	1. Non Secure Connect => ns_connect.
	    
	2. Non Secure Paste => ns_paste.
	    
	3. General Non Secure => gen_ns.
    
      
    

Function unmarkedSymptoms(database, comparison table, similarity rate, param):

This function fulfills two purposes, one, it  is used to count the total unmarked initial symptoms having connections (when param = 0), two , it is used to update the unmarked initial symptoms with zero comparative.

The `$unmarkedSymptomsArrayFinal[]` stores all the unmarked initials with zero comparatives. This array is also used for updating the “marked” field to “1” when saving a comparison.

The `$unmarkedSymptomsArrayFinalNumber[]` stores the initial ids having ongoing connections.