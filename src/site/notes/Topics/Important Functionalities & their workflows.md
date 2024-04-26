---
{"dg-publish":true,"permalink":"/topics/important-functionalities-and-their-workflows/"}
---


**Source type of a symptom:**

Source type can be assigned for a source using the Books option from the master database Menu Point or by changing the settings of "Symptomherkunft" under the the Symptom Type Setting Menu Point.

Source type are given values as primary, secondary and undefined. If source type of specific symptoms having provers and literature reference needs to be changed then this can be done using the Symptomherkunft option of the symptom type setting menu point.

Related PHP functions: fetchSourceTypeModified(symptom id, original quelle id, symptom end detection for t , tt and pallet)

and symptomEndIdentifyCheckForAlphaBetaAndT().

Basic Workflow:

1. fetchSourceTypeModified() function first searches for the source tyoe assignment from "quelle" sql table.
    
2. Then it searhces for assignment from "quelle_symptom_settings" sql table. By default the value is taken from "symptom_type_for_whole_origin" field of the sql table if present.
    
3. Checks if prover or reference is linked to the symptoms and accordingly the source type is updated from the values of "quelle_symptom_settings" sql table.
    

  

**Symptom type of a symptom:**

Symptom type can be assigned for a source using the settings of "Symptomart" under the the Symptom Type Setting Menu Point.

Symptom type are given values as proving, intoxication etc.

Related PHP functions: fetchSymptomTypeModified(symptom id, original quelle id, symptom end detection for t , tt and pallet)

and symptomEndIdentifyCheckForAlphaBetaAndT().

Basic Workflow:

1. fetchSymptomTypeModified() function first searches for the source tyoe assignment from "quelle_symptom_settings" sql table.
    
2. By default the value is taken from "symptom_type_for_whole_origin" field of the sql table if present.
    
3. Checks if prover or reference is linked to the symptoms and accordingly the source type is updated from the values of "quelle_symptom_settings" sql table.