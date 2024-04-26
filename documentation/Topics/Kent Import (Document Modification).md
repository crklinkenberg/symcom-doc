Kent source documents are special type of documents, and these documents need to be restructured to make it compatible for the importing its information.

Workflow of the editor:

1. The editor selects all the data from the Kent document and copies it.
    
2. Navigates to Kent Import menu point.
    
3. Pastes the copied data to the text editor.
    
4. Submits it. The program then modifies the submitted data, restructures it and the new modified Kent document is automatically downloaded in the browser.
    

  

Technical Flow:

                   a.  Submitted data is sent through method POST.

b.  PHP Word class is initialized.

                   c.  Each line is iterated.

d.  modifyKentTagsCapitalizeFirst() PHP function, extracts the HTML tags and makes the first character uppercase. This function only checks the text words from the first(one or two) tags of the string.

e.  The last occurrence of “(” and “)” is taken out and the page number is then extracted and appended to the front of the string with “@S: ”.

f.  Final modified line is then inserted in “$finalContentArray[]”. This array is then inserted in the word document by the program and the document is downloaded in the browser.