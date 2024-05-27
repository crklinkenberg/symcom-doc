---
{"dg-publish":true,"permalink":"/topics/chapter-assignment-modification/"}
---

Any edits required for assignment chapters or to delete any assigned chapter, mode 1 of the chapter assignment process can be used.

On click of Edit option in mode 1, new chapters can be selected from the drop downs. 
HTML id `chapterAssignSave` initiates the save process of the chapters assigned.
This id calls a JS function `saveAssignment()` which calls another PHP script `chapter-assignment-backend.php` via AJAX to perform the operation.

Clicking the cross icons beside the chapter name deleted the chapters.
HTML class `deleteChapter` is used for initiation of the delete process.

For non secure chapters, JS function `addnscNoteChapter()` is used.

Related PHP scrips:
```
chapter-assignment.php
chapter-assignment-backend.php
delete-chapter-assignment.php
chapter-function.js
```



