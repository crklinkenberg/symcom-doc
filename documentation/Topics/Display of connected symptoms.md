NOTE: In case of single source comparisons, the connections are displayed in order like: connect edit first, then connect, then paste edit and then paste.

  

In the case of combined source comparisons, the connections are displayed as per the latest connection order. This combined source when saved and converted to final completed version, the chronological order that is sorting in order of years (older year to newer) takes place.

  

Instant display of connected symptoms is controlled by individual scripts of connect.js, paste.js, connect-edit-exp.js, paste-edit.js.

  

Display of connected symptoms on load takes place with the help of “connectSave()” js function.

  

Symptom ids are kept in js arrays when loaded according to source type: single or combined. This arrays are:

  

- singleConnectionComparativeCheck
    
- singleConnectionInitialCheck
    
- combinedConnectionIntialsCheck
    
- combinedConnectionComparativeCheck
    

  

These arrays then send the ids for taking out information with the help of “symptom-connection-operations.php”  php script.

The response from this script is then send as parameters to js function connectSave() js function which controls all the display of connected symptoms.

Workflow of connect-saved.js script.

The “connectSave()” js function is contained in the connect-saved.js script.

  

Basic workflow:

- Switch case controls every connection case.
    
- First the initial and comparative HTML symptom text is created using the values of the parameters.
    
- The “source_type” parameters is detected. Source type can be “singleSourceInitial” which is for initials in single source comparison, “singleSourceComparative” for comparing symptoms in single source comparison, “combinedSourceInitials” for initials in combined source comparison, “combinedSourceComparative” for comparing symptoms in combined source comparisons.
    
- After this, the initials or comparing symptom ids are from the HTML DOM elements using jQuery based on their source type and are appended in the appropriate positions.
    
- After this, icons for info and linkage column and command columns are modified using “initialsWithComparativesConnectedBelow”, “comparativesWithInitialsConnectedBelow”, “initialsWithComparativesDisconnectedBelow”, “comparativesWithInitialsDisconnectedBelow” and “swapComparativesIcons” js functions.