---
{"dg-publish":true,"permalink":"/topics/reflexive-grades-with-c-es-and-swap-c-es/"}
---

#general #comparison 
### Scenario:
```
Let's say there is initial symptom X from source A and symptom is displaying normal texts with grade 1.

There is another symptom Y  from source B which is comparative symptom appearing below X and is displaying normal texts with grade 2.

If a CE (Connect Edit) is done and symptom X is connected with symptom Y, then by default the initial symptom X will apply the grades associated with its connected comparative symptom Y from source B. Thereby, displaying the normal text of symptom A in grade 2.

The same case can happen if CE is done with swap i.e. SWAP CE where the initial will consider the grades associated with its connected comparative symptom. 

This is the reflexivity of grades among connected symptom pairs with CEs and SWAP CEs.
```

By default, the grades applicable with CEs and SWAP CEs are reflexive unless a checkbox is activated to fix the grading during the connection process.  

*Below the checkbox is shown from the CE modal during comparison process.*

![Pasted image 20241221120117.png](/img/user/assets/Pasted%20image%2020241221120117.png)


### Technical Details:

Whenever CE or SWAP CEs are done, the gradings are considered as fixed and are fetched from `symptom_grading_settings` SQL table and is processed by `convertTheSymptom()` PHP function.

In order to make the gradings reflexive as per the connected comparative symptom, some modifications are done.

##### Saving of the CE and SWAP CE gradings to become reflexive:
1. A new flag `is_reflexive` is introduced in the `symptom_grading_settings` to save the connection for reflexive grades. The default value is '0' and for connections like CE and SWAP CE, the value is '1'. It is also added in the `temp_editable_symptom_grading_settings` SQL table which is responsible for showing grades in the preview option whenever CE and SWAP CE are done.
2. Whenever, CE or SWAP CE is done, the modal with text editor having HTML id `connectEditModal` is now introduced with a checkbox and if it is checked, the gradings are considered as fixed. The checked value is received in the backend script with name `fixed_ce_grade`. The default value is '1'. When checked, it is '0'.
3. The backend scripts responsible for the input from the modal are `connect-edit-operations.php` and `connect-swap-operations.php`.
4. After the connection is saved in the connections SQL table, when the gradings are saved by `updateEditedSymptomsSettings()` PHP function, the `fixed_ce_grade` flag value is passes through PHP array `gradingData[]` as an input field.
5. The PHP function `updateEditedSymptomsSettings()` further processes the input and is saved in the `symptom_grading_settings` SQL table.


##### Displaying of reflexive grades:
1. The display of the grades in the symptom texts are controlled by `convertTheSymptom()` PHP function. The input is an array and all input parameters are sent as key value pairs in the input array.
2. After initialization of the grades, the saved grade for that particular input is fetched from `symptom_grading_settings` SQL table and if the `is_reflexive` field is found active then the connections table for that comparison is first searched, the connected comparative symptom ID is taken out, the `original_quelle_id` field value is then fetched for that particular symptom ID from the dynamic comparison table. 
3. The `original_quelle_id` found is kept in PHP variable `sourceIdFound` and this value is used to fetch the grades from the `quelle_grading_settings` SQL table.
4. The grades fetched are then processed and the returned output displays the symptom text with the fetched grade values, thus maintaining its reflexivity.
5. If `is_edit_preview` input key value is found active then reflexivity flag `is_reflexive` is fetched from `temp_editable_symptom_grading_settings` SQL table and `original_quelle_id` is fetched as mentioned above.

##### Related scripts:
```
comparison-table-page-modals
functions.php
connect-edit-operations.php
connect-edit-exp.js
get-preview-of-connect-edited-symptom.php
connect-swap-operation.php 
```
