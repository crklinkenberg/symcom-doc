---
{"dg-publish":true,"permalink":"/topics/some-j-query-variables-and-function-name-with-their-usages/"}
---


Below are important jQuery variables and their usages for better understanding the program.

Js function interacts with backend PHP scripts for operations with the databases. Some important PHP scripts during connection process are:

- connect-swap-operation.php: used for swap operation with connect and connect-edit.
    
- connect-edit-operation.php: used for normal connect edit operations.
    
- paste-edit-operation.php: used for paste edit operations.
    
- connection-save-script.php: used for normal connect and paste operation.    
    

symptom-connection-operations.php: used for arrangement of connected symptoms on load.

| Variables                                                          | Usage                                                                                                                                                    |
| ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. earlierConnectionExist                                          | Used as a flag variable for earlier connection existence.                                                                                                |
| 2. earlierConnectionExistSwap                                      | Used as a flag variable for earlier swap connection existence.                                                                                           |
| 3. operationFlag                                                   | Flag used for connection operation of previous connected  symptoms with new parent. Has different values for connect, ce, paste, pe and  swaps.          |
| 4. previousSwapConnecectEdit                                       | Flag used for swap connection of previous swap connect  edit symptoms. Updating of symptom text done accordingly in the backend  script.                 |
| 5. sendingElement                                                  | The clicked html DOM element is taken here.                                                                                                              |
| 6. normalOperation(sendingElement)                                 | Js function for normal connect operation.                                                                                                                |
| 7. swapConnectOperation(sendingElement)                            | Js function for connect operation with swap.                                                                                                             |
| 8. arrayForEarlierConnection                                       | Array for previous connected symptoms, data are kept  here. Useful for sending data to backend scripts.                                                  |
| 9. earlierConnectionExistCe                                        | Used as a flag variable for earlier connection existence.                                                                                                |
| 10. ceModalDisplay                                                 | Flag variable to control the connect edit text editor pop  up.                                                                                           |
| 11. ceNormalOperation(ceModalDisplay,sendingElement)               | Js function for initializing normal connect edit  operation.                                                                                             |
| 12. swapConnectCeOperation(ceModalDisplay,sendingElement)          | Js function for initializing connect edit operation with  swap.                                                                                          |
| 13. ceModalDisplayFn(ceModalDisplay,sendingElement)                | Js function for connect edit operation with text editor  display On.                                                                                     |
| 14. connectEditOperation()                                         | Js function when connect edit connection process is  executed.                                                                                           |
| 15. connectEditSwapOperation()                                     | Js function when connect edit connection process is  executed with swap.                                                                                 |
| 16. $domComparative                                                | Js constant for extracting the DOM element of the  comparative symptom.                                                                                  |
| 17. $domInitial                                                    | Js constant for extracting the DOM element of the initial  symptom.                                                                                      |
| 18. saveConnects()                                                 | Js function for saving connect and paste connection in  database.                                                                                        |
| 19. free_flag                                                      | Kept as an extra variable for any paste connection  modification.                                                                                        |
| 20. deleteSymptoms(initial id,comparative id,disconnect operation) | Js function for disconnection normal paste and connect  connection.                                                                                      |
| 21. disconnectEarlierConnection()                                  | Js function for disconnection earlier connect connection.                                                                                                |
| 22. checkShellExecution()                                          | Js function to check the completion of table creation  process in background.                                                                            |
| 23. singleConnectionInitialCheck[]                                 | Js array for checking connection of symptoms with  initials.                                                                                             |
| 24. singleConnectionComparativeCheck[]                             | Js array for checking connection of symptoms with  comparatives.                                                                                         |
| 25. combinedConnectionIntialsCheck[]                               | Js array for checking connection of symptoms with  initials in combined source mode.                                                                     |
| 26. combinedConnectionComparativeCheck[]                           | Js array for checking connection of symptoms with  comparatives in combined source mode.                                                                 |
| 27. connectSave()                                                  | Js function which controls all connected symptoms when  page is loaded.                                                                                  |
| 28. connectionSort()                                               | This function  takes html element and helps in sorting of connected symptoms.<br><br>  <br><br>sorting order: connect-edit->connect->paste  edit->paste. |
| 29. symptomTextFilter(text)                                        | This function  is used for filtration of symptom text when translation is open.                                                                          |
| 30. reloadConnection()                                             | Reloading  function with URL modified when show all translation and connections open or  closed.                                                         |