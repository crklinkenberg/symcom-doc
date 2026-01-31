---
{"dg-publish":true,"permalink":"/topics/matched-percentage-and-highlighted-words-process-in-comparison-page/"}
---

#comparison 

Display of matched percentage is executed by a PHP function `newComareSymptom()` which is defined in the `“functions.php”` page.

  

1. The function is effective only when comparing symptom codes are executed in comparison page. This functions sends two parameters: the initial symptom text and the comparing symptom text.
    
2. The strings passed are first cleaned, removed any special characters, converted to lowercase and every word in symptom sentence is kept in an arrays. One for initial symptom and other for comparing symptom.
    
3. For the comparing symptom string, the words which are not “stop-words”, are kept in an array.
    
    “Stop words” are predefined words which prohibits the program from calculating matched percentage. These words are defined by the user. The “stop-words” panel can be accessed from the comparison page.
    
4. Both arrays are then filtered and words with greater than three characters are only kept.
    
5. The words are then intersected and unique words are only considered as matched.
    
6. First match for similar words are considered, then match searching for characters in other words are also done. Only the unique matches are then considered.
    
7. The matched words are then encapsulated with an HTML tag for adding highlights (styling).
    
8. Finally, word counts are taken and percentage is calculated for matched percentage. 
    
    (check the newComareSymptom() function in functions.php page for the calculations involved)