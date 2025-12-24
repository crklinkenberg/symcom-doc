---
{"dg-publish":true,"permalink":"/topics/individual-upgrade-of-symptoms/"}
---


Individual upgrade can be done from the comparison final view page.
Tinymce editor has been modified in `common.js` and new tiny mce editor has been defined for this individual upgrade of symptoms. 
All grade icons has been redefined.

Issues faced:
```
Symptom text changes. Integrity of the spaces after grade effect.

Showing correct grade with application of css properties defined in the symptom text.

Text management via css. Tiny mce helper function has been modified several times to reduce bugs.
```

Symptoms individually upgraded are stored in `edited_symptom_text_versions` SQL table. It is considered as fixed grade so modifications are done in the `convertTheSymptom()` PHP function so that it retrieves the individually upgraded symptom from `edited_symptom_text_versions` SQL table.

Related PHP functions:
```
updateSymptomAfterEdit()
getEditedSymptomText()

```