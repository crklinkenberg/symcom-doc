---
{"dg-publish":true,"permalink":"/topics/allen-source-import/"}
---

#import 

Allen Sources are special sources where symptoms have references linked to it. These references can also have provers who have worked with that particular literature.

Example of Allen source symptoms:

After eating he seems intoxicated, `[1]`.

Careless ease, such as is often produced by a small dose of hasheesh, `[24]`.

  

Here in both the symptoms the numbers in square brackets "1" and "24" refers to the literature linked to it. These numbers are defined on top of the source document inside a literature block. 

Example:

Literature start

@P:Hahnemann

1, Hahnemann, R. A. M. L., 2, 273

@P:Hornburg

3, Hahnemann, R. A. M. L., 2, 273

23, Davis, J. E. L, MS. proving, constant effect of the 3d dil.

24, Wenzel, Trans. of the Alumni Ass. of the Hasp. Coll. of Med., Louisville Med. News, 3, 114, 1877, doses of 10 drops of tincture three times a day, for several days

Literature end

  

Here, number "1" is linked with reference "Hahnemann, R. A. M. L., 2, 273" and the prover/tester associated with this literature is "Hahnemann". Similarly, number "24" is linked with reference " Wenzel, Trans. of the Alumni Ass. of the Hasp. Coll. of Med., Louisville Med. News, 3, 114, 1877, doses of 10 drops of tincture three times a day, for several days" and it is not linked to any provers as there is no direct ordering of provers before the literature with number "24".

  

NOTE: If a reference has multiple provers associated with a particular literature multiple direct ordering can be declared before the reference. Example:

  

Literature start

@P:First Prover

@P:Second Prover

1, Hahnemann, R. A. M. L., 2, 273

@P:Hornburg

3, Hahnemann, R. A. M. L., 2, 273

Literature end

  

Here, literture "1, Hahnemann, R. A. M. L., 2, 273" has multiple provers linked with it.

  

### Technical Details:

*Note: In the below details reference and literature mean the same.*

Manipulation of Allen source symptoms is done by the `importedStringManipulationProces()` PHP function which handles all the symptoms during import.

  
### Background:
Allen sources are special sources having `literature start` OR `literatur start` at the start of the document and `literature end` OR `literatur end` at the end of the document. It is imported from the same form where import of symptoms is done to the sources.

### Basic Workflow:
Step 1: Literature detection and store.

1. The literature block with strings literature start and literature end is detected.
    
2. The function is continued with "isContinue" flag.
    
3. Key "isPreDefinedReferenceSection" from "variablesArray" is used for furthur operation.
    
4. Checks if prover is defined with the help of "directOrderDetection()" function.
    
5. Provers found are stored in `prueferFromParray` key of the `variablesArray`.
    
6. The `referenceNumber` is detected and the reference is first searched if it is already present in the `literatures` SQL table. If present the id of the reference is taken out.
    
7. If literature is not present, new literature is inserted in the `literatures` SQL table and the ID is taken out.
    
8. The reference id, reference text, reference number detected and provers linked are kept in an array and this array is inserted to `preDefinedReferenceArray` key of the `variablesArray`.
    
9. As the program iterates through all the references and associated provers in the literature, all id's of the references with the reference number is stored in `preDefinedReferenceNumberArray` key of the `variablesArray`. This keys of this array are the literature numbers and the values are literature id's.
    

  

Step 2: Linking of literature with the symptoms.

1. As the program finishes the literature block with the prepared literatures in `preDefinedReferenceNumberArray` array. The program now continues iteration with all the symptoms.
    
2. In the process of symptom string manipulation towards the end of the function, the program searches for the values of `preDefinedReferenceNumberArray`.
    
3. If the literature number in the symptom string is found, it is encapsulated with `<sup>` html tags.
    
4. The literature id associated with that particular literature id is then linked.
    
5. Literature text is first stored in the `aLiteraturquellen` key of the `variablesArray` and then it is finally added to `EntnommenAus` key of the same array. After which it is further processed for insertion in `itemp_symptoms` table and then to `symptoms` SQL table.
    

  

Allen Source Import Symptoms in `symptoms.php` page.
![Pasted image 20240423164323.png](/img/user/assets/Pasted%20image%2020240423164323.png)

Related scripts:
```
functions.php
symptoms.php
```


