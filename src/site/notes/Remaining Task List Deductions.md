---
{"dg-publish":true,"permalink":"/remaining-task-list-deductions/"}
---


```
1. Individual upgrade of symptoms from comparison final view display list.
```

```
Trigerred with edit icon from the comparison final view page.
Edit only converted version.
Include all grade icons.
Saving in edited_symptom_text_versions SQL table.
Fetching from edited_symptom_text_versions for individually upgraded symptoms.
Changes in convertTheSymptom() function.
```

```
2. Edit of symptoms, original version, converted version from symptoms list after import. 
```

```
Triggered from edit icon of the symptoms page.
Edit both original and converted version option active.
Changes will be saved to symptoms table and the final comparison dynamic table.
There is an issue with the grades though. Only one version of edited grades are stored in the symptoms_grading_settings SQL table. So if, symptoms is edited after import then in some comparison, the symptoms is involved in connections like CE, then the previous edits which were done from the symptoms page will not exists, as the new grade version from CE will be saved in the SQL table. 

Questions:
Do you want to edit it before involvement of the source in comparison?

Alternative Solutions:
I think this edit icon can be removed from the symptoms page.
If any mistake is found, then there is option to remove it or deactivate it from the expert tool.
To add the symptom, we can use the "import symptoms under same source and remedy".
```

```
3. Addition of prover from CE text modal.
```

```
Curruently the detection of prover from CE text editor is not possible as CE text editor and its related backend scripts are programmed to only save the grades for parts of the symptoms involved.

To implement will also make the CE process quite complex.
We can however plan to do this, i.e addition of prover to the symptom from the expert tool.
```

```
4. Import of symptoms under the same source and remedy name. 
```

```
When same source and medicine is detected. The values will be retrieved from the SQL quelle_import_master SQL table.
Then check if the source is involved in comparison and if, completed version is available.
If available then it will be inserted to the symptoms and the final version dynamic SQL tables in the same settings.
If source is not involved in comparsion then insert in the symptoms table.
If source is involved in comparison but completed version is not made, then return false, exit the operation.

Important:
The import settings should be exactly the same.

Questions:
Import of symptoms under the same source and remedy name
=> What would happen if a source say X is imported, compared with three comparing sources A, B, C and then new symptoms are imported?
In the program we will have comparisons for :
X_A
X_A_B
X_A_B_C

If new symptoms are inserted now then it will part of the new source "X_A_B_C"
where X will contain both its original symptoms and new imported symptoms.

Situation: What if the editor sees mistakes and decides to re-activate comparison "X_A_B". In this case the new imported symptoms will not be available as the new symptoms was only added to the last comparison source "X_A_B_C".


If we have to add the new symptoms to all other previous comparisons, then new comparisons needed to be made which would be technically inefficient.

Alternative Solution:
I think import of symptoms or addition of symptoms should only be added to the symptoms SQL table and to the final version dynamic table.
In this way, the imported new symptoms will be visible or will be operational from next consequtive comparisons but will not be available for the comparisons which has already been done earlier. It is the only efficient and reasonable way.
```


```
5. Import of Heilmittelarchiv sources.
```

```
For this task we need some plannings. 
Must come to a common ground. The source should follow the symcom minimum requirments or should be manipulated in some form.

We need to add a book with some pre defined author and year.
Only in this way, it is possible.
But I also need to know if there are any more requirements.
```

```
6. Expert tool after final save 
```

```
Outside of comparison, i.e. in completed SQl table.
Disconnection amongst symptoms.
Connection amongst symptoms. All connection.
General edits, like edit of text?
Deletion of symptoms. (Could this be deactivaton?)

Work arounds:
Expert tool button in final view.
On click, temporary completed table along with connections table will be created from the original tables.
A new webpage will show the final version with abilities to disconnect, checkboxes with all symptoms, toolbar with delete, general edit, to make it as comparative (white symptom), add special data like prover, author, reference.
Save button in expert tool webpage, to implement those changes.
Work with expert tool can be resumed if not saved and opened again later.
```

```
15. Chronological sorting of symptoms in the comparison.
```

```
Case:
Chronological sorting has been defined differently for active working comparisons and the finalized comparison version.

For the working comparison, the connections are sorted as per connections. Like in this order (CE, connect, PE, paste)

For saved finalized comparison list, the connections are sorted as per the year.

Question:
The connection in the working comparison needs to be chronologically sorted as per the year?

NOTE: It will not be simple to maintain each element. Deep JS coding is required. Will take some time. [2 weeks]
```
