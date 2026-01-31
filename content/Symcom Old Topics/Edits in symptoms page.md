---
{"dg-publish":true,"permalink":"/topics/edits-in-symptoms-page/"}
---


Edits can be done for bracket contents, testers, footnotes, chapters and references in the symptoms webpage.

Associated scripts:
```
assets/js/common.js
dev-exp/functions.php
dev-exp/get-all-provers.php
dev-exp/symptoms.php
dev-exp/save-edits-of-symptoms.php
```

Important PHP functions associated:
```
fetchMultipleRows()
updateSymptom()
editExecutionInSymptomsPage()
getAllTesters()
```

Important JS functions associated:
```
getAllProvers()
saveProverAfterEdit()
```

NOTE: `edit-icon` class is added in each html element where edit is enabled.
This is then controlled by `symptom-edit-cancel-btn` and `symptom-edit-save-btn` html classes and JS events.