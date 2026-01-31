---
{"dg-publish":true,"permalink":"/topics/chapter-classification-model-re-train/"}
---

#chaptering 

Chapter classification model re-training can be done uploading a `.txt` file containing the chapter name and symptoms in particular format. The format is like this:
```
Chapter: Main Chapter Name
Symptom ...
Symptom ...
SubChapter: Sub Chapter Name
Symptom ...
Symptom ...
SubsubChapter: Sub Sub Chapter Name
Symptom ...
Symptom ...
```

This file can be automatically generated for each compared and chapter classified comparisons using the "Download File for Model Re-train" menu option from chapter assignment mode 1 and mode 2 pages.

The file downloaded can be uploaded to train the model using "Model Re-train" menu option. The language should also be appropriately selected in this process.
![Pasted image 20240610172803.png](assets/images/Pasted%20image%2020240610172803.png)

Backend Scripts:
```
chapter-download-file-for-model-re-train.php
chapter-upload-file-for-model-re-train.php
```

Workflow involved in download process:
 1. Once file down option is clicked, upon confirmation, modal with id `chapterFileGenerationModal` is initiated and displayed. This modal constitutes of a html form and submission is handled by the `chapter-download-file-for-model-re-train.php` backend script.
 2. Main chapter, sub chapter and sub sub chapter are taken out after selection of data from `chapter` column from the completed table of the particular comparison.
 3. Files created are first saved in location `/comparison-writing/` and then is deleted after the download process is successful.

Workflow involved in upload process:
1. Once the modal for chapter model re-train is submitting via form with id `chapterFileUploadForm` it is handled via AJAX. 
2. The file and language input are taken to the backend script `chapter-upload-file-for-model-re-train.php`.
3. API call on `"http://www.dev.reference-repertory.com:8000/<language>/upload?language=$lang"` is done to train the model.
4. On success, the user is notified with a message.