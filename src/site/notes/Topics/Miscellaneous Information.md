---
{"dg-publish":true,"permalink":"/topics/miscellaneous-information/"}
---


1. Comparison Loading: New HTML id "bodyst" is added to the comparison page. Whenever navigation is done in comparison page or comparison is opened from materia medica page, the comparison page will directly scroll to the above id and display the comparison.

  

2. Connection Business Logic Validation: The backend validation of connection business logic was modified. PHP function "connectionBusinessLogicCheck()" controls the backend validation now and is added in all connection related scripts.


3. Green plus and minus icon colors for initial symptoms having active connection along with earlier connection:
    

In symptom-connection-operations.php script, wheen the rows of a particular initials are selected, the "is_earlier_connection" field is searched from the connections table and is checked if its value is "0", which will mean that particular initial has current active connection. So only initials id with current active connections are kept inside this array.

  

The initial id and the current connection exists check are then kept in an array "currentConnectionExistsArr" which is returned as response.

  

The response is taken in the comparison page and for each of the initial ids, the "toggleInitial" html class is searched and if "earlierSavedConnection" class exists then "earlierSavedConnection" class is removed.

  

Associated scripts:

comparison.php

comparison-super.php

symptom-connection-operations.php

  

NOTE: This opertions are only work for combined initials symptoms. Refer to the "symptom-connection-operations.php" scripts for more details.

**Longer Session Fix:**
Both "session.gc_maxlifetime" and "session_set_cookie_params" does not seem to work.
A logic with timestamp is implemented in the route script.

But the full fix was done, by changing the phpini script in server both at the server php location and in the apache root folder.

  

Server side fixed by: server admin.

Related scripts:

config/route.php

config/route-staging.php

config/route-production.php