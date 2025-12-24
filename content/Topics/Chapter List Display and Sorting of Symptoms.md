---
{"dg-publish":true,"permalink":"/topics/chapter-list-display-and-sorting-of-symptoms/"}
---

#chaptering 
#### Chapter List Display
The `symptom-chapter-list.php` script displays the assigned symptoms in order of the chapter structure. At max ten chapters can be displayed in this web page, PHP variable `$perPageChapterHead` controls the chapter head display.

The list displayed in this web page is provided with a “sort” icon for each chapter names. Clicking this button, redirects the program to the symptom sorting page.

#### Sorting of symptoms within a chapter:
The `chapter-sort-symptoms.php` script is associated with sorting of symptoms within a chapter. Symptoms can be clicked and dragged and drop at any location to sort it. The latest changed symptoms is shown in darker green color and the its previous place in lighter green color just after the drag and drop operation. jQuery function `sortable()` is used for sorting and retrieving the sorting data in frontend.

Technical workflow of sorting of symptoms;
1. The symptom is dragged and dropped.
2. Ajax request is sent to `chapter-sort-symptom-backend.php` script with `newPositions` array which contains the symptom ids of the new arrangement.
3. As per the data from `newPositions` array, the `arrangement_order` column from the `symptom_chapter_assignment` SQL table is updated to follow the new order. This column is responsible for display of the symptoms within a chapter in the saved order.