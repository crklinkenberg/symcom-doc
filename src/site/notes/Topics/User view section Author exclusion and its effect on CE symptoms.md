---
{"dg-publish":true,"permalink":"/topics/user-view-section-author-exclusion-and-its-effect-on-ce-symptoms/"}
---


In the user view section, we have our final symptom list displayed. Here we have option to exclude an author, according to which all symptoms of the excluded author will be removed from the displayed symptom list in the user view section.

Here when we have a CE symptom in the user view section and we exclude the author of the CE symptom then the CE effect of the symptom is also gets removed from the symptom and the symptom is displayed in previous state (the state before the CE).

**Technical Workflow:**

When we deselect an author form the user view filtration options section, through function “fetchExcludedAuthors()” we fetch the deselected authors, Then we collect the source/quelle ids of the deselected authors with the help of the author and source/quelle relationship table “quelle_autor”. Now we have the quelle_id(s) of the deselected/excluded authors. So now when displaying the symptoms we exclude the symptoms of these quelle_id(s).

Now when the deselected author is a CE symptom’s author, here also we have the quelle_id(s) of the deselected author that we have collected following the same above-mentioned process. Here we exclude the symptoms from displaying which belongs to the these excluded authors quelle_id(s) as mentioned above,

now for each symptom which are going to be displayed (means the symptom which don’t belongs to the excluded authors quelle_id(s)), with the help of function “fetchOriginalQuelleOfConnectedSymptom()” we collect the connect edited symptom’s quelle_id, if the displaying symptom is a CE symptom. Now again we check if this quelle_id is in excluded authors quelle_id(s), and If the result is yes, then we collect the previous state of this connect edited symptom with the help of the function “fetchCEdataOfSymptom()” and display this sate of the symptom to the user in the web browser,

Here also we remove the excluded author’s part from the source name of the displaying symptom in the user view section with the help of function “getQuelleAbbreviation()”.        

Related scripts:

dev-exp/functions.php

dev-exp/user-view/index.php

dev-exp/user-view/user-views/symptom-list.php

dev-exp/user-view/user-includes/user-functions.php