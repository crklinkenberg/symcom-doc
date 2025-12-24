---
{"dg-publish":true,"permalink":"/topics/navigating-to-initial-symptoms-from-search-window/"}
---


```
Scripts involved:
assets/js/dataTablesConfig.js
comparison.php
comparison-super.php
connection-function.js


Workflow:
Navigation is possible after clicking with mouse along with the ALT key from keyboard.

The comparison webpage is reloaded and scrolled to the selected initial symptom.

The initial serial ID is used for detection of the initial symptom via JS.
The page to be navigated is calculated:
initial serial ID selected / per page initial symptoms.

The ceil value is the page.


JS functions involved:
searchFunctionData()
addParamsAndRedirect()
removeParamsWithoutReload()

NOTE: URL parameters are modified. 
Params: custom_listing, ns_to_sent, ns_editing, gen_ns_to_sent are removed which are associted with NS listings.

These params are removed as navigation inside the NS list is not possible as the initial symptom might not appear in the list.

The scrolling is handled in the comaparison.php and comparison-super.php scripts.
```