---
{"dg-publish":true,"permalink":"/symcom-v2-documentation/resolution-of-slowness-symcom-current-version-vs-new-version/"}
---


The slowness as reported by client has been mainly encountered in the comparison page.
Upon thorough analysis, it has been found out that the factors like loading of connections of each symptom and reloading of comparison webpage upon successful operations like CE and PE were majorly responsible.

In the current Symcom version, connections are loaded in the below mentioned approach:
```
Step 1: Each of the initial symptom ids and comparing symptoms ids are kept in separate PHP arrays during page load.
```
```php
$singleConnectionsInitials = array();
$singleConnectionsComparative = array();
```

```
Step 2: These arrays are converted and made compatible as JS arrays.
```
```php
$singleConnectionsComparativeString = (!empty($singleConnectionsComparative)) ? implode(',', $singleConnectionsComparative) : "";
```

```js
 var singleConnectionComparativeCheck = [<?php echo $singleConnectionsComparativeString; ?>];

var singleConnectionInitialCheck = [<?php echo $singleConnectionsInitialsString; ?>];
```

```
Step 3: These arrays are then sent as parameters in JS functions which performs ajax calls to a backend PHP script, which goes through each of the symptom ids in the array, perfoms SQL operations for each of them, fetches connections and sends back the response with connection data to another JS function which makes the html element for each of the connected symptom and attaches the html element in the comparison webpage.
```

```
Step 4: Comments, footnotes or translations are furthur loaded into after connections are attached in the webpage.
```

This whole operation of taking each symptom ids, connecting to backend script with ajax and attaching the returned response as html elements in the webpage takes much time if many initial symptoms and comparing symptoms are loaded in the webpage which slows down the page reloading operation.

<hr>

### Improvements in the new Symcom version

In the new version, loading of connections are not done via JS and ajax calls. When symptoms are loaded from the PHP script, a function is called which checks and loads connections for each of the symptom, so there is no waiting for connections after webpage is loaded once in the browser.

Any operations of connections like connect, CE, PE, paste or swaps do not reload the webpage. Only the affected symptoms pairs are modified via JS and CSS.

Improvements were already implemented in the highlighting function for matched words. Each symptom ids are checked with asynchronous JS functions and highlights are added to the symptom texts. These JS functions as compared to the existing versions, do not wait for the whole page to load, and execute in the background and highlights are loaded as user scrolls through the page.

Moreover, for the comparison page, previously used html attributes and elements but which are obsolete now are being removed. Html elements for the initial and comparing symptoms are now simpler with less elements and data attributes which reduces the load time.

Loading of comparatives in batches has been implemented like the current version, with improved modifications for highlights function.

Furthermore, the new version of Symcom has refactored database due to which there are less calls for queries and operations as compared to the current version.  
