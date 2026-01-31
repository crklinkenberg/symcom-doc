Initial serial numbers is shown with all the initials in the comparison page. Since this number serves as an ID for the initial symptom in the comparison page and is used frequently by the editors, its state is preserved i.e the initial serial number does not change even if per page initial symptoms is changed or the listing of the initial symptom is modified by filtration like NS listings.

`initial_serial_number` field is added to the comparison SQL table and is added during the comparison process. 

Related scripts:
```
create-dynamic-comparison-table.php
create-dynamic-initial-insertion-restart.php
```

Basic workflow for assignment:
```
Since the initial symptoms are sent for computation in batches.
At the start of the batch processing process in the create-dynamic-comparison-table.php script, initialSerialNo is initialized to 0.

In this script call to create-dynamic-initial-insertion-restart.php script takes place, where the initialSerialNo variable is incremented for each initials, inserted to the dynamic comparison table and is then returned as a respose to the parent script i.e create-dynamic-comparison-table.php.

```

The PHP variable used is `initialSerialNo`.