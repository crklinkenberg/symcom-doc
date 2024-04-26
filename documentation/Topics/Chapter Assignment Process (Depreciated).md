Completed comparisons with green status in the materia medica page is displayed with a “list” icon along with the title. This icon can be clicked to start the chapter assignment process. There are two modes of chapter assignment “mode 1” and “mode 2”.

Mode 2: The default mode is 2 and this shows the symptoms one by one. Symptoms can be assigned chapters with weights here. The webpage is provided with Final, Save and NS buttons. Final button finalizes the assignment and navigates to the next symptom. The NS button helps in assigning doubtful chapters (non secure).

Mode 1: This mode displays the symptoms in list. At present it displays max 100 results in one page. This webpage is also provided with an “info” icon which displays the symptom information.

Both modes are provided with edit functionality and a navigation bar with “change language”, “show chapter list”, “show NS unassigned”, “show all symptoms” and “reset” buttons.

NOTE: Whenever chapter assignment icon is clicked from materia medica page, the  unassigned symptoms are shown first, in order to view all the symptoms from the source, “show all symptom” button can be used and to reset to default view, the “reset” button is used.

  

Chapter Assignment Process (Technical Help):

For mode 1, “chapter-assignment.php” script is used.

PHP flag “$show_all_ns_unassigned” is used for showing all the ns and unassigned symptoms.

PHP function “checkIfNoAssignedSymptomExist(completed_table_name)”  is used to check if any unassigned chapters exist in the source.

The id’s returned by SQL query is kept in a PHP array “$arrayWithAllUnassignedIds[]”. This id is the used for fetching symptom information.

Below are HTML form id used for different processes.

|   |   |   |
|---|---|---|
|Id|Associated with|Note|
|assignForm|Language change||
|assignSaveForm|Saving, editing.||
|showAllSymptomForm|showing all symptoms,||
|showWithResetForm|reset||
|autoListForm|Change to mode 2|Target script: chapter-assignment-auto.php|
|showNSSymptomsForm|Showing non secure and unassigned symptoms.||
|showChapterListForm|Go to chapter listing page.|Target script: symptom-chapter-list.php|

  

For mode 2, “chapter-assignment-auto.php” script is used.

The “$displayPageId” PHP variable is used to scroll and display the active symptom on top of the web browser when mode is changed from 2 to 1.

Database association: The completed table of the source is used for assigning chapters.

Display of chapter list:

The “symptom-chapter-list.php” script displays the assigned symptoms in order of the chapter structure. At max three chapters can be displayed in this web page, PHP variable “$perPageChapterHead” controls the chapter head display.

The list displayed in this web page is provided with a “sort” icon for each chapter names. Clicking this button, redirects the program to the symptom sorting page.

Sorting of symptoms within a chapter:

The “chapter-sort-symptoms.php” script is associated with sorting of symptoms within a chapter. Symptoms can be clicked and dragged and drop at any location to sort it. The latest changed symptoms is shown in darker green color and the its previous place in lighter green color just after the drag and drop operation. Jquey function “sortable” is used for sorting and retrieving the sorting data in frontend.

Technical workflow of sorting of symptoms;

1. The symptom is dragged and dropped.

2. Ajax request is sent to "chapter-sort-symptom-backend.php" script where the sorting array from sortable function, the json filename and the abbreviation of the chapter head are sent as parameters.

3. In the backend script, the json filename is first retrieved, decoded, the chapterHeadArray[] is replaced with the sorting array sent, the chapter head array is then replaced, encoded and saved in the “chapter-data” directory.

  

Important PHP functions associated with the chapter assignment process:

|                                 |                                                                        |                                                                                                                                                                                                 |
| ------------------------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Function name                   | Purpose                                                                | Parameters Sent                                                                                                                                                                                 |
| getArzneiTitelInChapter         | Get arznei title.                                                      | arzneiId                                                                                                                                                                                        |
| checkIfNoAssignedSymptomExist   | Check if unassigned chapter exist.                                     | completedTable                                                                                                                                                                                  |
| chapterExplodedStringOperation  | Display assigned chapters of a particular  symptom in required format. | Chapter string, chapter head array in English,  chapter head array in German, chapter head abbreviation, symptom  id, chapter weight, id from sql table.                                        |
| chapterHeadPagination           | Used to display chapter heads in symptom  chapter listing webpage.     | Pagination start value, Per page chapter head  , total chapters int value, chapter abbreviation array, table Name, Chapter  string, chapter head array in English, chapter head array in German |
| getChapterInformationForChapter | Retrieve symptom information                                           | Original Quelle Id, symptom Id                                                                                                                                                                  |