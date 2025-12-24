---
{"dg-publish":true,"permalink":"/topics/unmatched-symptoms-comparison/"}
---


Comparison for unmatched symptoms is asked on saving a comparison with save button after verification and checks of non secure symptoms, general non secure symptoms and unmarked initial symptoms.

Start with click event from `comparison-table-save-btn` html class.
Associated scripts:
```
comparison.php
comparison-super.php
```

Int value 6 is sent as parameter to JS function `savingComparison(6).

`savingComparison()` submits the save form with id `saveSubmit`.

It updates input with id `temp_unmark_check` to the param value.

Gets assigned to PHP variable `unmarkedInitialsCheck` in PHP scripts.
According code sections for `unmarkedInitialsCheck` value 6 is executed where comparison result instead shown with unmatched comparatives symptoms.


`