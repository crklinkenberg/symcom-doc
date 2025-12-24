---
{"dg-publish":true,"permalink":"/topics/punctuation-removal-from-grading/"}
---

#general 

Punctuation removal from grading is done by modifying the symptom string having customized html tags. The main idea is to remove the punctuation symbols encapsulated between any html tags, keeping the string intact, that is maintaining the integrity of the tag contents.

  
Punctuation in here refers to these symbols: `'.', ',', ':', ';', '?', '!', '(', ')', '[', ']'`.


Other characters are not taken into consideration here as symbols like "-" (hyphen), "'" (apostrophe), "''"(quotation marks) and "..."(ellipsis) can arise conflict with the customized tags which helps in the grading process.

  
Punctuation removal is done just before display of the symptoms after the conversion process. The related function is: `punctuationPositionFix()` which is included in the `functions.php` script.


This function takes the input string as a parameter and splits the string into smaller parts where the punctuations occurs with the help of a regex pattern. The sub parts are stored in an array.
  

Each of these parts are processed and checked for below categories:

1. If both open and closed html tags are present in the sub part.
    
2. If only open tag is present in the sub part.
    
3. If only closed tag is present in the sub part.
    
4. If no tag are present in the sub part.


Consecutive occurrences of punctuation are also checked before manipulation of the html tags in each part.

```
Below showing a simple illustration:

  

Input String = "I have <strong> fever, cough </strong> and <em>headache. Sometimes stomach ache</em>";

  

Processed String = "I have <strong> fever</strong>,<strong> cough </strong> and <em>headache</em>.<em> Sometimes stomach ache</em>";
```
This function solves the problem of inclusion of punctuation in the gradings and replacement of redundant spaces between comma and dot with just a dot when displaying.
