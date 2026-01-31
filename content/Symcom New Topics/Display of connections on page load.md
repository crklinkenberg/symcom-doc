The display of connection is done directly by manipulating the main PHP script.
The main comparison page follows a hybrid pattern where both PHP and html elements are rendered as per PHP logic.

The chronological ordering is also handled by the HTML DOM structure in the comparison web page.

Below is the structure for initial symptom:
```html
<div class="symptom"></div>
<div class="ongoingConnections_100">
	<div class="comparativesConnectedCE"></div>
	<div class="comparativesConnectedCD"></div>
	<div class="comparativesConnectedPE"></div>
	<div class="comparativesConnectedPASTE"></div>
</div>
<div class="previousConnections_100">
	<div class="comparativesConnectedCE"></div>
	<div class="comparativesConnectedCD"></div>
</div>
```

The ongoing connections is appended in the classes staring with `comparativesConnected` inside classes which starts with `ongoingConnections_100`, here 100 is the initial symptom number id.

Below is the structure for comparative symptom:
```html
<div class="symptom"></div>
<div class="ongoingConnections_200">
	<div class="initialsConnectedCE"></div>
	<div class="initialsConnectedCD"></div>
	<div class="initialsConnectedPE"></div>
	<div class="initialsConnectedPASTE"></div>
</div>
<div class="previousConnections_200">
	<div class="initialsConnectedCE"></div>
	<div class="initialsConnectedCD"></div>
</div>
```

The chronological ordering is maintained via the HTML DOM structure. For ongoing connections, the connect edits are shown first then connect then paste edited connections and then paste for a particular initial symptom.

When page is loaded, PHP function calls are done to check if the symptoms are involved in connections, upon successful verification, the symptoms are manipulated as per their connections in the page itself. This reduces slowness previously faced when loading connections by calling JS scripts again during page load.

Some important PHP functions involved in loading connections in the comparison page:
```
checkConnectionForSymptom()
=> checks if the symptom is involved in connections. If symptoms is involved in comparison then plus, minus icons are appened to display or unhide the connections below it. By default the connections remain hidden.

checkInitialSymptomIdOfLatestConnection()
=> checks the initial symptom id of the latest connection from the comparison. This is used to open or unhide the last connections done in the comparison.

getConnectedRowsHtmlInComparisonPage()
=> connected symptom is fetched from connections table, made into an html element for appending in the classes starting with "comparativesConnected".

checkConnectionForComparativeWithInitialSymptom()
=> checks if the comparative symptom has connection with the initial symptom above it.
```

Related scripts:
```
dev-exp/functions.php
dev-exp/comparison/index.php
dev-exp/assets/css/comparison-table-styles.css
```

