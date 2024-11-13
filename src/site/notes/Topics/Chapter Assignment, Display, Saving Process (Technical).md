---
{"dg-publish":true,"permalink":"/topics/chapter-assignment-display-saving-process-technical/"}
---

#chaptering 
#### Automatic assignment process:
Chapters are automatically assigned by the chapter classification python program. 
The python program is called via an API through PHP function `fetchChapterForSymptom()`. This function in turn call `recursionArr()` PHP function which separates the primary chapters, primary more chapters and secondary chapters based on the API response.

The assigned chapter ids are saved in the database in the completed SQL table of the comparison in a particular format. 

`Primary chapters ##&## Primary More Chapters ##&## Secondary Chapters ##&## Tertiary Chapters`.

Also, chapters are saved in the `symptom_chapter_assignment` SQL table which plays an important role during ordering of symptoms within a particular chapter. 

More on the python chapter classification program. Check here:
[[Topics/Chapter Classification Python Program\|Chapter Classification Python Program]]

Related-scripts:
```
chapter-assignment-initiation.php
materia-medica.php
```

Once this process is complete, for any modification of assigned chapter mode 1 and mode 2 of the chapter assignment process can be used.

SQL column value of `chapter_assigned_complete` from the `pre_comparison_master_data` SQL table is checked if the automatic assignment process is complete.

*Important:*
*When automatic assignment process is running, please make sure no other functionality of the chapter classification program should be used else the python server might throw an error.*
#### Mode 1 of chapter assignment process
`chapter-assignment.php` script is used.
PHP flag `$show_all_ns_unassigned` is used for showing all the ns and unassigned symptoms.

PHP function `checkIfNoAssignedSymptomExist(completed_table_name)`  is used to check if any unassigned chapters exist in the source.

The id’s returned by SQL query is kept in a PHP array `$arrayWithAllUnassignedIds[]`. This id is the used for fetching symptom information.

Below are HTML form id used for different processes.

|                     |                                             |                                            |
| ------------------- | ------------------------------------------- | ------------------------------------------ |
| Id                  | Associated with                             | Note                                       |
| assignForm          | Language change                             |                                            |
| assignSaveForm      | Saving, editing.                            |                                            |
| showAllSymptomForm  | showing all symptoms,                       |                                            |
| showWithResetForm   | reset                                       |                                            |
| autoListForm        | Change to mode 2                            | Target script: chapter-assignment-auto.php |
| showNSSymptomsForm  | Showing non secure and unassigned symptoms. |                                            |
| showChapterListForm | Go to chapter listing page.                 | Target script: symptom-chapter-list.php    |

#### Display of chapter structure and their id's 
Each chapter returned by the `getAllChapters()` PHP function is given an id. This id is then saved in the `chapter` column of the `completed_table` SQL table of the comparison.

Suffix "_MC" is added to main chapters, "_SC" to sub chapters and "_SSC" to sub sub chapters.

#### Saving of chapter assignment in the database:
The id's of the chapters are saved in the `chapter` column of the `completed_table` SQL table of the comparison.  Chapters assignment of weights namely primary, primary more, secondary and tertiary are  saved in the `chapter` column separated by a delimiter `##&##`.

For example if assigned primary chapter is "01_MC", assigned primary more chapters are "02_MC, 05_SC", secondary chapters are "01_SC, 04_SC, 07_SSC", then the `chapter` value in the SQL table will be:

`01_MC ##&##  02_MC, 05_SC ##&## 01_SC, 04_SC, 07_SSC ##&## ##&##`\
which is of the form: 
`Primary chapters ##&## Primary More Chapters ##&## Secondary Chapters ##&## Tertiary Chapters`.

Related Scripts: 
```
chapter-assignment-backend.php
```

#### Mode 2 of chapter assignment process
`chapter-assignment-auto.php` script is used.
The `$displayPageId` PHP variable is used to scroll and display the active symptom on top of the web browser when mode is changed from 2 to 1.

Important PHP functions associated with the chapter assignment process:

|                                 |                                                  |                                |
| ------------------------------- | ------------------------------------------------ | ------------------------------ |
| Function name                   | Purpose                                          | Parameters Sent                |
| getArzneiTitelInChapter         | Get arznei title.                                | arzneiId                       |
| checkIfNoAssignedSymptomExist   | Check if unassigned chapter exist.               | completedTable                 |
| getChapterInformationForChapter | Retrieve symptom information                     | Original Quelle Id, symptom Id |
| getAllChapters                  | Get all chapters name as per structure.          |                                |
| fetchChapterName                | Fetch the chapter name from the chapters tables. | Chapter Id Array               |