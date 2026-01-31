For large source all the comparatives are not loaded at once and can instead be loaded in batches. For this a "Load More" button appears with the comparative symptom set for under each initials. 

By default fifteen comparatives are loaded. "Load More" button is displayed if more comparatives matches under initial symptom.

`Div` element with class `load_more_comparatives` is added.
On clicking this element, the event is handled by `connection-page-function.js` script.


### Related JavaScript:
```
getComparativeDataInBatches() => generates the next batch via PHP scripts and ajax call.

After the batch is successfully generated, the highlighting of the matched words are done after JS promise via processHighlightingOfSymptoms() function.


After highlighting is done, then loading of associated connections for the comparatives is done via loadConnectionsForSymptoms() function.

After this comments, footnotes and translations are loaded with commentsOnLoadFn(), footnoteOnLoadFn(), translationOnLoadFn() functions for each comparative symptom. Everyhting is handled via JS promises.


JS : getComparativeDataInBatches()
Script: generate-comparative-batch.php
PHP function: getTotalComparativesOfSingleInitialSymptom(), generateComparativeBatch()

```

### Related PHP:
```
Script: generate-comparative-batch.php

PHP function: 
getTotalComparativesOfSingleInitialSymptom()
generateComparativeBatch()
fetchRows()
getInitialSymptomsAllSynonyms()
```