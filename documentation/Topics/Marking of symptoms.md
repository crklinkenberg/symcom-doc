In the comparison listing, with all initial symptoms there is a check box for marking. This is for quality assurance of the whole comparison during editing. Marking rules:

- In fresh state of comparison, all initials will be marked unchecked. However, the initials with no comparatives are directly shown as marked by the program.
    
- When connections are made with an initial, the checkbox is shown as marked.
    
- Initial having comparatives but no connections are made by the editor, in this case the editor will have to mark the checkbox voluntarily.
    
- Comparison with unmarked symptoms is not allowed to saved.
    

Technical Details:

Marking is controlled both in the front end part and in backend.

  

Front-end:

For initials symptoms with no comparatives, the marking is done with the help of js.

- During the process of listing of symptoms when comparison page is loaded, the initials with “marked” value “0” is stored in PHP array `$markSymptomIds[]`.
    
- This array is then converted to js array “markSymptomIdsFinalArray[]”. For each of the ids in this array, comparatives are checked below each initial id’s, if no comparatives are found then the marking checkbox is marked.
    
- Also, for each of these initials with no comparatives, the general non secure connect button is disabled.
    

Back-end:

- When marking checkbox is checked or unchecked by the user, ajax call is made to “update-marking-symptoms.php” script. Initial id, comparison table and marked Value (0 or 1) is sent as parameters here.
    
- This scripts updates the “marked” field in the comparison table.