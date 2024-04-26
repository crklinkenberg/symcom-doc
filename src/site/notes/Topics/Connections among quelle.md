---
{"dg-publish":true,"permalink":"/topics/connections-among-quelle/"}
---


Connections for comparative symptoms under initial symptoms can be done in the icons under “Command” column. All codes for connections are available in separate JavaScript files.

Connections like connect, disconnect, non-secure connect, non-secure paste, paste, paste edit and connect-edit can be done. All connections are happening following connection rules.

Other than connections, all symptoms can be added a comment, footnote, searched for its German/English translation and edited with icons under “Info & Linkage” column.

Below are the technical steps followed when connections/disconnections are done:

- Connect (Connection):
    

1. When connect button is clicked in the command icon group, with the help of “connect” class, a jQuery function is initiated.
    
2. Initial symptom ID, comparing symptom ID, language, initial and comparing year are all extracted.
    
3. The program follows the business logic and accordingly starts checking the extracted variables or shows popups to prevent connection.
    
4. If the initial year is greater than the comparing year then SWAP connect connection operation starts.
    
5. If the initial year is equal to the comparing year then the user is shown a pop up message and option for swap connect, normal connect or just escape is given.
    
6. If the initial year is smaller than the comparing then normal connect opeartion starts.
    
7. For normal connection normalOperation() function is used. The clicked DOM element is send as a parameter for further operation.
    

	1. Inside the function the values extracted from the initial and comparing symptom are then sent through a jquery function “saveConnects()”.
	    
	    Function saveConnects() takes the below parameters:
	    
	    Connection Type, comparative ID, Initial ID, comparison language , connected percentage,  comparative symptom text, initial symptom text, comparing quelle code, initial quelle code, comparing year, encoded comparing symptom text de, encoded comparing symptom text en, comparing quelle original language, comparing quelle id, initial year, encoded initial symptom text de, encoded initial symptom en, initial quelle id, initial quelle original language.
	    
	2. After this DOM manipulation takes place with the help of jquery.
    
	    NOTE: Comparative symptoms after connection is kept inside the “comparativesConnectedCD” class. Initial symptoms after connection is kept inside the “initialsConnectedCD” class when displayed in HTML format.
    

9. For swap connection swapConnectOperation() function is used. The clicked DOM element is send as a parameter for further operation.
    

	1. If any previous connections are found in the intial or the comparing symptom, then the previous connection details are kept inside an jquery array arrayForEarlierConnection[].
	    
	2. All extracted values like ids of the symptoms and arrays are then sent to “connect-swap-operation.php” via an ajax request for further operations and savings in the connection sql table.
	    
	    Brief workflow of “connect-swap-operation.php” script:
    

		This function then sends the parameters to “connection-save-script.php” and saves the function parameters in connections SQL table via ajax call.

  

		- Input received is validated.
		    
		- The SQL table field with “symptom_id” matching to the initial id is updated:
		    
		
		- swap => 1
		    
		- swap_value_de => The comparing symptom string in German text.
		    
		- Swap_value_en -> The comparing symptom string in English text.
		    
		
		- The “id” of the initial symptom is fetched.
		    
		- The subsequent “id” is stored in PHP variable `$rowIdToInsertFrom`.
		    
		- All information of the initail id is taken out and stored in a PHP array `$connectionDataArray`.
		    
		- The row fields of the comparing symptom id are updated with initial symptom texts, including the value of “swap” equals to “1”.
		    
		- All comparing symptoms under the initial symptom are selected, then comparing symptom texts are compared with the changed initial symptom.
		    
		- The compared results are then stored in PHP array `$data`.
		    
		- If the “symptom_id” and “initial_symptom_id” of the comparing symptom equals to the initial id that was sent as a parameter, then the “symptom_id” including other fields like “quelle_code”, “quelle_titel” etc of the initial symptom id are updated with the values of that particular comparing symptom. Here the initial id is now fully swapped with the information of the swapped comparing symptom id.
		    
		- The symptom id information which were in the `$data` array are then sorted and stored in the `$completeSendingArray` PHP array.
		    
		- Based on value of the `$operationFlag`, the ids in the `$arrayForEarlierConnection` array are compared with the initial and then stored in the array `$earlierConnectionSaveArrayFinal`.
		    
		- The ids from the `$completeSendingArray` array are then appended below the initial id. (The comparing symptoms below the initial are at first deleted and then the new ids and information are inserted).
		    
		- The ids from `$earlierConnectionSaveArrayFinal` array are updated in the connection sql table based on the values of `$operationFlag`.
		    
		- The id’s with new highest matched percentages are then updated in the highest matches table.
		    
		
		On successful completion of the ajax request, the page is reloaded.

- Connect (Disconnection):
    

1. On clicking disconnect button, with the help of “disconnect” class, a jQuery function is initiated.
    
2. The program checks if SWAP connect connection exists, if not then below steps are followed.
    

	1. The program first shows a pop up confirming the user’s input for disconnection operation.
	    
	2. Disconnection can happen both from “comparativesConnectedCD” and “initialsConnectedCD” HTML classes. In both the cases the below steps are followed:
	    
	
		1. The “deleteSymptoms()” function sends the initial symptom ID and comparative symptom ID as parameters to “connection-delete-script.php” for backend disconnection from the connections SQL table.
		    
		2. The program checks if the connection is from previously connected connection with the help of “earlierConnection” class.
		    
		3. If the connection has “earlierConnection” class then the connected initial ID and the symptom ID is passed as parameter to “disconnectEarlierConnection()” functions. More details on this functions later in this documentation.
		    
	
	3. After this the DOM manipulation takes place with the help of jquery.
    

3. If swap connection exist while disconnection, then below steps are followed:
    

	1. Disconnection of the swap connect can be done from the “comparativesConnectedCD” and “initialsConnectedCD” class. In each of the cases, below steps are followed.
	    
	
		1. Values are extracted and sent to “connect-swap-operation.php” via an ajax request for further operations in the connection SQL table. (Swap disconnection process is same as swap connection, the symptom values are reversed and the existing swap connection is deleted form the connection table).
		    
		2. After successful ajax request, the page is reloaded.
    

- Connect Edit (Connection):
    

1. When connect edit (CE) button is clicked, all the information of initial and comparing symptom is extracted with the help of  “symptom-connect-edit-btn” HTML class.
    
2. If the initial symptom year is greater than the comparing symptom year the swap connect edit takes place.
    
3. If the initial year is equal to the comparing year then the user is shown a pop up message and option for swap connect-edit, normal connect-edit or just escape is given.
    
4. If initial symptom year is smaller than the comparing symptom year then normal connect edit operation takes place.
    
5. Normal connect-edit operation takes place with help of ceNormalOperation() js function. While, the swap connect-edit operation is initiated by swapConnectCeOperation() js function. Both of these functions sends the clicked element as a parameter along with a flag “ceModalDisplay”. Both these functions calls ceModalDisplayFn() js function.
    
6. The ceModalDisplayFn() function displays the editor inside a pop up. It extracts the values necessary for the connect edit operation, also keeps the previous connections in an array arrayForEarlierConnection[] if found.
    
7. On editing of the initial symptom and submitting the connect edit modal, a jquery function is initiated with the help of “connect-edit-modal-submit-btn” class.
    
8. If the flag value of “swapCheck” is “1” then SWAP connect edit connection operation starts. The connectEditSwapOperation() js function is called. Inside the function the extracted values along with arrays is sent to “connect-swap-operation.php” for further operation in the mysql databases.
    
    NOTE: Steps for swap connect edit is same as swap connect. In the first steps, the initial symptom which is to be swapped is first checked if the initial has already been swapped (this is the case if the initial has previous swap connection and connection is possible), accordingly the sql field of the comparison table is updated with new text values and swap connect edit is further processed. In case of swap, all the comparing symptoms under that initial are checked and compared again, existing comparing symptoms are deleted and new comparing symptoms are inserted.
    
9. If the flag value of “swapCheck” is “0” then  normal connect edit operation starts. The function connectEditOperation() is called.  The program then follows the below steps.
    
10. The “connectEditOperation()” function takes initial symptom ID, comparative symptom ID, cut off percentage, edited initial symptom text, comparison language, comparison option, comparison table name and operation type as parameters and sends it to “connect-edit-operation.php” to perform backend operation. After successful completion of the backend operation, the comparison page is reloaded. 
    
    Brief workflow of “connect-edit-operation.php” script:
    
11. Input received is validated.
    
12. The SQL table field of the comparison table is updated:
    

1. final_version_de => edited initial symptom text in german.
    
2. final_version_en => edited initial symptom text in english.
    
3. is_final_version_available => 1.
    

14. The id field from the comparison table having the initial symptom ID is taken out and is incremented by one and stored in a PHP variable `$rowIdToInsertFrom`.
    
15. All information of the initial symptom ID  is taken out in arrays.
    
    NOTE: PHP array `$connectionDataArray` is used for storing informations of the initial symptom and the comparing symptoms in the connections SQL table.
    
16. The comparing symptoms which is connected under that initial symptom is selected, and the comparing string is compared with the new edited initial symptom string.
    
17. If the new matched percentage is higher then the pervious matched percentage then the symptom ID of the comparing symptom is stored in `$updateHighestMatchSymptomIdArray` PHP array.
    
18. After this, the comparing symptoms along with all updated information are stored in a PHP array “$data”.
    
19. All symptoms are then sorted according to the new matched percentage and are then copied to PHP array `$completeSendingArray`.
    
20. All the comparing symptoms under that initial are then deleted.
    
21. Insertion of the new updated comparing symptoms are done from the `$completeSendingArray` PHP array.
    
22. Insertion of the updated initial and the connected comparing symptom data are then inserted in the connections SQL table.
    
23. The highest matches table is then updated with the values from `$updateHighestMatchSymptomIdArray` PHP array.
    
    NOTE: Comparative symptoms after connection of connect edit is kept inside the “comparativesConnectedCE” HTML class. Initial symptoms after connection of connect edit is kept inside the “initialsConnectedCE” HTML class.
    

If initial is already swapped (previous connection), then accordingly other swap fields are updated instead of final version fields in the sql table.

  

- Connect Edit (Disconnection):
    

1. When connect edit (CE) button is clicked for disconnection, the “disconnectCE” class calls a jquery function.
    
2. The user is first prompted with a pop up, on confirming the disconnection, the below steps takes place.
    
3. When connection is disconnected from comparaing symptom under “comparativesConnectedCE” or  “initialsConnectedCE” HTML class, below steps stakes place.
    

	1. The program extracts the ID’s of the comparing and the connected initial symptom.
	    
	2. Checks if the connection is from previously connected connection with the help of “earlierConnection” class.
	    
	3. If the connection has “earlierConnection” class then the connected initial ID and the symptom ID is passed as parameter to “deleteSymptoms()” and “disconnectEarlierConnection()” functions. More details on these two functions later in this documentation.
	    
	4. If the connection is not an earlier connection then all the comparatives under that initial is first removed and a loader is shown.
	    
	5. The “connectEditDisconnectOperation()” function is called with parameters initial ID, comparing ID, cut off percentage, comparison option and comparison table name. The function then sends it to “connect-edit-operation.php” to perform backend operation. On successful execution, the comparison page is reloaded.
	    
	    Workflow of “connect-edit-operation.php” script during disconnection is same as connect edit connection but the SQL fields “final_version_de”, “final_version_en”  are updated to NULL and “is_final_version_available” is updated to 0.  Rest process are all same except, insertion in the connection SQL is not done only deletion of the connect edit symptoms for that particular initial ID and comparing ID is done.
    

4. If the disconnection of connect-edit connection is done for swap connect-edited connection then connectEditDisconnectSwapOperation() function is used for further operation. It acts same like the connectEditDisconnectOperation() function.
    

- Paste (Connection):
    

1. When paste button is clicked in the command icon group, with the help of “symptom-paste-btn” HTML class, a jQuery function is initiated.
    
2. The program follows the business logic and accordingly follows.
    
3. Initial symptom ID, comparing symptom ID, language, initial and comparing symptom texts are all extracted.
    
4. All values extracted from the initial and comparing symptom are then sent through a jQuery function “saveConnects()”.
    
5. The functioning of the saveConnects() function is same as in the case of connect connection.
    
6. After this DOM manipulation takes place with the help of jQuery.
    
    NOTE: Comparative symptoms after connection is kept inside the “comparativesConnectedPASTE”HTML  class. Initial symptoms after connection is kept inside the “initialsConnectedPASTE”HTML class when displayed.
    

- Paste (Disconnection):
    

1. On clicking disconnect button , with the help of “disconnectPaste” HTML class, a jquery function is initiated.
    
2. The program first shows a pop up confirming the user’s input for disconnection operation.
    
3. If the comparing symptom is inside the “comparativesConnectedPASTE” class then the below steps are followed.
    

	1. The program checks if the connection is from previously connected connection with the help of “earlierConnection” class.
	    
	2. If the connection has class “earlierConnection”  then deleteSymptoms() function sends initial symptom ID, comparing symptom ID along with operation=’paste’ as parameters to “connection-delete-script.php” for backend disconnection from the connections SQL table. After successful execution the page is reloaded.
	    
	3. If the connection does not have class “earlierConnection”  then deleteSymptoms() function sends initial symptom ID, comparing symptom ID as parameters to “connection-delete-script.php” for backend disconnection from the connections SQL table. After this the DOM manipulation takes place with the help of jquery.
    

		The “deleteSymptoms()” function sends its parameters (initial symptom ID, comparing symptom ID, operation) to “connection-delete-script.php”.

  

		This function deletes connection between the symptoms in the connection SQL table and in the cases of paste and paste-edit, it updates the ‘connection’ field of the comparison table to ‘0’ if no connect and connect edit connections are found for the initial symptom ID in the connections SQL table.

  

- Paste Edit (Connection):
    

1. When paste edit (PE) button is clicked, all the information of initial and comparing symptom is extarcted with the help of  “symptom- paste-edit-btn” HTML class.
    
2. Any previous connection connected with the comparing symptom is taken inside the array “arrayForEarlierConnection[]”.
    
3. The values extracted are then sent to “paste-edit-operation.php” via ajax request for backend operation with MySQL table.
    
4. After this DOM manipulation takes place with the help of jQuery.
    
5. If the source type is of combined, then the page is reloaded.
    

- Paste Edit (Disconnection):
    

1. On clicking disconnect button , with the help of “disconnectPE” class, a jQuery function is initiated.
    
2. The program first shows a pop up confirming the user’s input for disconnection operation.
    
3. The program then extracts the ids and other values required for disconnection and then sends to the “paste-edit-operation.php” via an ajax request for backend operation.
    
4. After successful operation DOM manipulation takes place with the help of jQuery.
    

	1. For connect:
	    
	    The “connection” field in the comparison table is updated to “0” for that particular previous connected symptom. The connection is deleted from the connections table.
	    
	2. For connect-edit:
	    
	    Fields like “connection”, “is_final_version_available”, “swap_ce”,” swap” are all updated to “0” in the comparison table for that particular previous connected symptom.
	    
	    Fields like “final_version_de”, ”final_version_en”, ”swap_value_ce_de”, ” swap_value_ce_en”,” swap_value_de”, “swap_value_en” are updated to “NULL” for that particular previous connected symptom.
    

		NOTE: The disconnectEarlierConnection() function disconnects the previously connected connections in case of connect and connect-edit. Initial symptom id, Comparing symptom id and the connection type(CE or connect) is taken as parameter here.