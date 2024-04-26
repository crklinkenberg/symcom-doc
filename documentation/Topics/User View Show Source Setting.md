![[Pasted image 20240423163127.png]]

Technical Details:

Source Setting is controlled by getQuelleAbbreviation() PHP function. Quelle id of the symptom, an array containing quelle id of the connected symptom and and option for switch case is sent as parameter in this function.

  

Work flow of this function:

Quelle id from  input is used to fetch information of author abbreviation, title abbreviation and year.

Multiple authors are concatenated and displayed.

If  the symptom has connect edit or swap connect edit connection then the quelle id of the connected symptom is also sent in the array with key "ce_swapce_symptoms_quelle_id".

Information fetching for the connected symptom is same like its parent.

If connect edit or swap connections are found then the source code is separated by a "/" between the parent symptom source and connected symptom source.

Example:
![[Pasted image 20240423163141.png]]

In this particular set, teh fourth symptom has been connect edited.

Souce code of the symptom: PPMJvPKN 1867 , here PPM(author abbreviation) JvP(author abbreviation) KN(title abbreviation one) 1867(year).

Source code of the connected symptom: SchwPPMEN1879, here Schw(author abbreviation) PPM(author abbreviation) EN(title abbreviation one) 1879(year).

  

Related scripts:

functions.php

symptom-list.php