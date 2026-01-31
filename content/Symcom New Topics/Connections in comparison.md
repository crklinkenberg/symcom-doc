Connections and disconnections among the symptoms can be done in the comparison page.
Connections could be:
```
1. connect => normal connect.
2. connect edit => connect and edit of the initial symptom.
3. paste => pasting a comparative symptom.
4. paste edit => pasting with editing of comparative symptom. In general symptom is shortened with paste edit.
5. connect swap => connecting and swapping the pairs.
6. connect edit swap => connecting with initial symptom editing and swapping the pairs.
```

For each of these connection operations, disconnections are also available to revert back the connection performed.

Connections follows business rules:
For ongoing connection:

1. Comparing symptom after connect, further connect can be done with that symptom appearing under other initials.
    
2. Comparing symptom after connect, further paste and paste-edit cannot be done with that symptom appearing under other initials.
    
3. Comparing symptom after connect-edit, further connect can be done with that symptom appearing under other initials.
    
4. Comparing symptom after connect-edit, further paste and paste-edit cannot be done with that symptom appearing under other initials.
    
5. Multiple connect-edit can be done under same initial.
    
6. Comparing symptom after paste, further connect, connect-edit, paste and paste-edit cannot be done with that symptom appearing under other initials.
    
7. Comparing symptom after paste-edit, further connect, connect-edit, paste and paste-edit cannot be done with that symptom appearing under other initials.
    
8. Comparing symptom after swap connect or swap connect-edit, further connect, connect-edit, paste and paste-edit cannot be done with that symptom appearing under other initials.
    
9. If initial symptom has ongoing connection then no swap connect or swap connect-edit connection is possible.
    
10. If swap connect or swap connect-edit is done with one initial, no further connections or disconnections are possible with the other comparing symptoms appearing under that initial.
    

For previous connection:

1. If a comparing symptom has previous connection like connect, connect-edit or swap and if this comparing symptom is connected with the initial via any connection like connect, connect-edit, paste and paste-edit, then the previous connections will also get connected to the initial.
    
2. If initial symptom has previous connection like connect, connect-edit or swap, then after connection of the initial with a comparing symptom, the previous connection of the initial symptom will remain in the same previous connection state.
    
3. Disconnection of a previous connected symptom will make the symptom a free symptom and the symptom will appear as initial symptom or comparing symptom depending on the source in which it belonged.
    
4. Any previous connection like connect, connect-edit and swap will not be affected and would act normally in all connection.
    
5. All connections between initial and comparing symptoms happens at one-to-one level. When comparing symptoms with previous connections are performed any connections, then the previous relationships die and new connection with initial symptom is established.
    

Important Points on Disconnection of Edited Connections:

1. If an edited connection is disconnected that is if disconnection is done on connect-edit, swap connect edit connections then the symptom will go back to its previous state, which means previous grading which was effective on the symptom before that connection will be active.
    
2. If a comparing symptom has previous connections as its children and the comparing symptom is connected to the initial, then for the initial symptom, the children of the comparing symptoms becomes step children and disconnection among st any of these step children will not affect the state of the initial or comparing symptom.
    

Additional Notes: 
1. After the comparison is saved, if the saved source is again used as initial or comparing source in a new comparison then the connections in that source will be shown as previous connections.

2. The pasted connections appear after the initial symptom when the comparison is finally saved. When a comparison is saved, all the initial and comparing symptoms are combined to form one source which is called as a combined source. This source sorts initial symptoms and then the symptoms of the comparative source. The pasted connections appear in place below which initial they were pasted and does not appear in next comparison as previous connections.

### Technical Details:
#### Connections:
When connections are done, the html elements for connections are first handled by JavaScript, the saving is then done by PHP scripts. The front-end manipulation of the symptoms is done using jQuery.

Related scripts:
```
dev-exp/comparison/assets/js/connect.js
dev-exp/comparison/assets/js/connect-edit.js
dev-exp/comparison/assets/js/paste.js
dev-exp/comparison/assets/js/paste-edit.js
dev-exp/comparison/assets/js/comparison-page-functions.js

dev-exp/comparison/connection-save-script.php
dev-exp/comparison/connect-edit-operations.php
dev-exp/comparison/connect-swap-operations.php
dev-exp/comparison/paste-edit-operations.php
```


1. When icons for connections are clicked, it is first handled by on click JS events, which is then operated by `handleConnectionsOfSymptoms()` function. This function takes the parent element and comparative element and then validates the connection with `validateBusinessLogicOfConnections()` function.
2. Upon successful validation, the connection is first saved in the back-end via JS functions mentioned below.


| JS function name for saving in the back-end | Connection type | Related PHP script          |
| ------------------------------------------- | --------------- | --------------------------- |
| savingConnectionInBackend                   | connect         | connection-save-script.php  |
| savingPasteConnectionInBackend              | paste           | connection-save-script.php  |
| savingConnectionOfSwapsInBackend            | connect swap    | connect-swap-operations.php |
| savingConnectEditConnectionInBackend        | connect edit    | connect-edit-operations.php |
| savingPasteEditConnectionInBackend          | paste edit      | paste-edit-operations.php   |

3. The saving for connections of connect-edit and paste-edit is handled differently by  `handleConnectionsOfSymptoms()` function. For connect-edit, the text editor is first dynamically generated using `connectEditTextEditorGenerationOperation()` function. For paste-edit, text editor is first generated by `pasteEditTextEditorGenerationOperation()` function.
   
   More on this is [[Tiny MCE text editor for connect edit]]
4. The saving is then processed by `savingConnectEditConnectionInBackend()` for connect-edit and `savingPasteEditConnectionInBackend()` for paste edit.
5. Upon successful saving of connection by `handleConnectionsOfSymptoms()`, the symptoms are connected in the front-end via `processConnectionOfSymptoms()` function. This function takes the initial symptom as parent and comparative symptom and then performs jQuery operations, including additional display modification to correctly display the connection in the comparison page. 
6. For swap connections like swap connect and swap connect edit, after saving of connection via `savingConnectionOfSwapsInBackend()`, the comparative symptoms shown below the initial symptom changes, and it is first operated by `fetchComparativeSymptomRowsDuringConnection()` JS function and then the comparative symptom batch is generated by `getComparativeDataInBatches()` function. 

### Disconnections:
1. After click on the disconnection icons, it is first handled by JS event on click and then is operated by `handleDisconnectionsOfSymptoms()` function.
2. This function first validates if disconnection is doable via `validateBusinessLogicOfConnections()` function and then it is further operated by `savingConnectionInBackend()` function for disconnection of connect and `savingPasteConnectionInBackend()` function for disconnection of paste.
3. Disconnection for connect edit connection is done via `savingConnectEditConnectionInBackend()` function and `savingPasteEditConnectionInBackend()` function for paste edit.
4. After successful disconnection in the back-end by `handleDisconnectionsOfSymptoms()` function, the front-end modification of the connection is done via `processDisconnectionOfSymptoms()` function.