---
{"dg-publish":true,"permalink":"/topics/some-j-query-variables-and-function-name-with-their-usages/"}
---

#comparison 

| Variables                                                      | Usage                                                                                                                                         |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| earlierConnectionExist                                         | Used as a flag variable for earlier connection existence.                                                                                     |
| earlierConnectionExistSwap                                     | Used as a flag variable for earlier swap connection existence.                                                                                |
| operationFlag                                                  | Flag used for connection operation of previous connected symptoms with new parent. Has different values for connect, ce, paste, pe and swaps. |
| previousSwapConnecectEdit                                      | Flag used for swap connection of previous swap connect edit symptoms. Updating of symptom text done accordingly in the backend script.        |
| sendingElement                                                 | The clicked html DOM element is taken here.                                                                                                   |
| normalOperation(sendingElement)                                | Js function for normal connect operation.                                                                                                     |
| swapConnectOperation(sendingElement)                           | Js function for connect operation with swap.                                                                                                  |
| arrayForEarlierConnection                                      | Array for previous connected symptoms, data are kept here. Useful for sending data to backend scripts.                                        |
| earlierConnectionExistCe                                       | Used as a flag variable for earlier connection existence.                                                                                     |
| ceModalDisplay                                                 | Flag variable to control the connect edit text editor pop up.                                                                                 |
| ceNormalOperation(ceModalDisplay,sendingElement)               | Js function for initializing normal connect edit operation.                                                                                   |
| swapConnectCeOperation(ceModalDisplay,sendingElement)          | Js function for initializing connect edit operation with swap.                                                                                |
| ceModalDisplayFn(ceModalDisplay,sendingElement)                | Js function for connect edit operation with text editor display On.                                                                           |
| connectEditOperation()                                         | Js function when connect edit connection process is executed.                                                                                 |
| connectEditSwapOperation()                                     | Js function when connect edit connection process is executed with swap.                                                                       |
| `$domComparative`                                              | Js constant for extracting the DOM element of the comparative symptom.                                                                        |
| `$domInitial`                                                  | Js constant for extracting the DOM element of the initial symptom.                                                                            |
| saveConnects()                                                 | Js function for saving connect and paste connection in database.                                                                              |
| free_flag                                                      | Kept as an extra variable for any paste connection modification.                                                                              |
| deleteSymptoms(initial id,comparative id,disconnect operation) | Js function for disconnection normal paste and connect connection.                                                                            |
| disconnectEarlierConnection()                                  | Js function for disconnection earlier connect connection.                                                                                     |
| `checkShellExecution()`                                        | Js function to check the completion of table creation process in background.                                                                  |
| `singleConnectionInitialCheck[]`                               | Js array for checking connection of symptoms with initials.                                                                                   |
| `singleConnectionComparativeCheck[]`                           | Js array for checking connection of symptoms with comparatives.                                                                               |
| `combinedConnectionIntialsCheck[]`                             | Js array for checking connection of symptoms with initials in combined source mode.                                                           |
| `combinedConnectionComparativeCheck[]`                         | Js array for checking connection of symptoms with comparatives in combined source mode.                                                       |
| connectSave()                                                  | Js function which controls all connected symptoms when page is loaded.                                                                        |
| connectionSort()                                               | This function takes html element and helps in sorting of connected symptoms.<br><br>sorting order: connect-edit->connect->paste edit->paste.  |
| symptomTextFilter(text)                                        | This function is used for filtration of symptom text when translation is open.                                                                |
| reloadConnection()                                             | Reloading function with URL modified when show all translation and connections open or closed.                                                |
| onRmm                                                          | Push final comparison final version to user view section.                                                                                     |
| deleteTheComparison()                                          | Function to delete comaprison.                                                                                                                |
| deleteTheQuelle()                                              | Function to delete source.                                                                                                                    |
| initialsWithComparativesDisconnectedBelow()                    | Function to change icons of info & linkage during disconnection.                                                                              |
| comparativesWithInitialsDisconnectedBelow()                    | Function to change icons of info & linkage during disconnection.                                                                              |
| initialsWithComparativesConnectedBelow()                       | Function to change icons of info &  linkage during connection.                                                                                |
| comparativesWithInitialsConnectedBelow()                       | Function to change icons of info during connection.                                                                                           |
| markingFunctionOnDisconnection()                               | Function for checkmark of  initial symptoms during disconnection                                                                              |
| genNsFunctionOnDisconnection()                                 | General non secure function on page load.                                                                                                     |
| connectEditDisconnectSwapOperation()                           | Disconnection of connect edit swap connection.                                                                                                |
| connectEditDisconnectOperation()                               | Disconnect connect edit connection.                                                                                                           |
| swapConnectCeOperation()                                       | Swap connection function for connect edit connection.                                                                                         |
| deleteSymptoms()                                               | Disconnect function for normal connect and paste symptoms.                                                                                    |
| genNsOnLoadFn()                                                | General non secure icon control on page load.                                                                                                 |
| nonSecureOnLoad()                                              | Non secure icon control on page load.                                                                                                         |
| translationOnLoadFn()                                          | Translation control on page load.                                                                                                             |
| footnoteOnLoadFn()                                             | Footnote control on page load.                                                                                                                |
| commentsOnLoadFn()                                             | Comments control on page load.                                                                                                                |

#### JS with backend scripts during connection process:

Js function interacts with backend PHP scripts for operations with the databases. Some important PHP scripts during connection process are:

- connect-swap-operation.php: used for swap operation with connect and connect-edit.
- connect-edit-operation.php: used for normal connect edit operations.
- paste-edit-operation.php: used for paste edit operations.
- connection-save-script.php: used for normal connect and paste operation.    
- connection-save-script-earlier.php: used for earlier connect and paste symptom operation. 
- symptom-connection-operations.php: used for arrangement of connected symptoms on page load.

#### Important html class, id names:

| class, id                     | description                                                                      |
| ----------------------------- | -------------------------------------------------------------------------------- |
| comparativesConnectedCD       | connect connections under initial symptom.                                       |
| comparativesConnectedCE       | connect edit connections under initial symptom.                                  |
| comparativesConnectedPASTE    | paste connections under initial symptom.                                         |
| comparativesConnectedPE       | paste edit connections under initial symptom.                                    |
| initialsConnectedCD           | connect connections under comparing symptom.                                     |
| initialsConnectedCE           | connect edit connections under comparing symptom.                                |
| initialsConnectedPASTE        | paste connections under comparing symptom.                                       |
| initialsConnectedPE           | paste edit connections under comparing symptom.                                  |
| onRmm                         | Push of final comparison to reference materia medica which is user view section. |
| disconnectPE                  | Disconnect Paste Edit connection.                                                |
| disconnectPaste               | Disconnect Paste connection.                                                     |
| disconnectCE                  | Disconnect connect edit connection.                                              |
| connect-edit-modal-submit-btn | Connect edit modal submission.                                                   |
| check_custom_ns               | Check if comparison page is in non secure connection section.                    |
| all_initial_translation       | Show all initial translation checkbox.                                           |
| all_comparative_translation   | Show all comparatives translation checkbox.                                      |
| symptom-translation-btn       | Symptom translation icon to handle event.                                        |
| all-connections               | Show all connections.                                                            |
| marking                       | Marking of initial symptom event handle.                                         |

