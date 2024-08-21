---
{"dg-publish":true,"permalink":"/automatic-symptom-connection-process/"}
---


This process is available in the comparison process where an editor can choose to connect the highest matched comparative with the initial symptoms choosing a minimum percentage as lower limit for the automatic connection. Automatic connection only does normal connect connection.

![Pasted image 20240821121729.png](/img/user/Pasted%20image%2020240821121729.png)

Some details of the automatic connection process.
1. The automatic connection process for comparatives with 100% match or identical pairs (where initial and comparative symptom both have same symptom text and same text format) starts at the time when new comparison process is initiated. These connections appears directly in the comparison page.
2. When no current connections are made in the comparison page, a notice is shown to the editor to initiate the automatic connection process. If agreed, the editor is asked for automatic connection percentage and referred to the automatic connections page where all comparatives with highest match will be connected.
3. A total of 100 initial symptoms are displayed in the automatic connection page. The editor has the option to view symptom info, translation or disconnect any connection.
4. Only cases where no swap connections are possible or comparatives which does not have any previous connections are considered for the automatic connection process.
5. If any time the automatic connection listing page is closed or the review process is cancelled, the editor is automatically redirected to the automatic connections page when the comparison is opened from the `materia medica` page.
### Backend Operations (Automatic Symptom Connections):
From `create-dynamic-comparison-table.php` script:
1. A temporary table for connections is created dynamically.
2. The script `automatic-connection-of-symptoms-during-comparison.php` is called using `shell_exec()`.

From `automatic-connection-of-symptoms-during-comparison.php` script:
1. Comparison table, absolute URL and editor initials are taken as input parameters.
2. Execution for automatic connections are done from the initial symptoms in the main comparison table using batch processing method where initial symptoms are taken in batches of 10.
3. For each batch call to `automatic-connection-of-symptoms-per-batch.php` script is done via `shell_exec()`.

From `automatic-connection-of-symptoms-per-batch.php` script:
1. Symptom information are collected for the initial symptom.
2. Symptom information for the comparative with highest match percentage with the initial is taken out.
3. Both the symptom string of initial and comparative are sent as parameters to `checkIfIdenticalSymptomPairs()` PHP function to check if 100% identical match exists between the pairs.
4. The swap cases and comparatives having previous connections are excluded. `checkIfPreviuousConnection()` PHP function is used for checking if previous connections exists with the comparative symptom. 
5. For each initial and comparative pair, all information required for insertion of information in the connections table is taken in a PHP array.
6. The array is then sent to `connection-save-script.php` via `curl_exec()` which does the connection and inserts into the connections table.

From `connection-save-script.php` script:
1. Input parameter `connect_type` is used for the connect connections.
2. If input parameter `check_if_identical_pairs` is  `true` and automatic connection flag `automatic_connection` is `true`, then connections is inserted in the connections table.
3. If input parameter `check_if_identical_pairs` is  `false` and automatic connection flag `automatic_connection` is `true`, then connections is inserted in the temporary connections table.
4. If in case, editor proceeds with manual connection then `deleteTemporaryConnectionTable()` PHP function deletes the temporary connections table and sets `editor_connection_process` flag to 0 in `pre_comparison_master_data` SQL table.

### Backend Operations (Automatic Symptom Connections List Display):
From `comparison.php` script:
1. The automatic connection button with id = `editor_connection_process` displays a HTML modal with id = `automaticConnectionConfiguration` on click. This modal on submission redirects the editor to the `automatic-connection-list-view.php` script.
2. If manual connection is done in the comparison this button is disabled. The button is controlled both from frontend and backend. The button enabling and disabling classes are controlled by `checkTemporaryConnectionTable()` PHP function.

From `automatic-connection-list-view.php` script:
1. If no temporary connections table is found, this script redirects the editor back to the comparison page.
2. This scripts updates the `editor_connection_process` field of the `pre_comparison_master_data` to 1 based on the id of the table.
3. The connections are retrieved from the temporary connections table for that particular comparison.
4. Per page 100 initial symptoms are shown and the display of symptoms and their connections are similar to the work flows from the comparison page. The scripts involved are:
	1. `symptom-connection-operations-for-automatic-connections.php`
	2. `allIconFunctions2-jay.js`
	3. `connect-saved-for-automatic-list.js`
5. If disconnection of automatic connected symptoms is done by the editor then the flag `is_disconnected_by_editor` is set to 1 in the temporary connections table. This operation is execution by the connection backend script `connection-save-script.php`.
6. The finalization of the automatic connections can be done using the button with id = `finalize_connection_process`.
7. This button on click after confirmation, redirects the editor to `automatic-connections-migration-script.php`.

From `automatic-connections-migration-script.php` script:
1. All connections from the temporary connections table are taken based on `is_disconnected_by_editor` = 0.
2. The selected automatic connections are then taken in a PHP array `connectionsRowDataArray` and each of them are then inserted to the connections table of the comparison.
3. The temporary connections table is then deleted.
4. `editor_connection_process` flag in the `pre_comparison_master_data` is then set to 0.
