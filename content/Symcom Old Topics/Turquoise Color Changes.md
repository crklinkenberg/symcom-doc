---
{"dg-publish":true,"permalink":"/topics/turquoise-color-changes/"}
---


Italics or gradings 2 with html classes `text-grade-2` has been shown with a turquoise color.
Related scripts:
```
comparison.php
comparison-super.php
```

Turquoise color added only to comparatives in the comparison.
Changes from JS:
```js
const observer = new MutationObserver(function () {
	$('.text-grade-2').not('.initial .text-grade-2').css('color', '#017373');
});
```

It is also added to the comparative symptoms loaded with the Load More button for large comparisons.

Additional Related scripts:
```
dev-exp/assets/js/comparison-page-functions.js
dev-exp/comparison-history.php
```

New JS variable `connections_script` introduced in the JS script.
It takes value from input element with id `connections_script` in the PHP scripts.
It is then passed to `loadConnectionsForSymptoms()` JS function.

Additional Changes in JS:
```js
// Observe changes to the body or a specific container
observer.observe(document.body, {
	childList: true,
	subtree: true
});
```
