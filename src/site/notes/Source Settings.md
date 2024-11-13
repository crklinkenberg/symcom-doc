---
{"dg-publish":true,"permalink":"/source-settings/"}
---


# Gradings
#### Technical Details:
Grade Settings shows the list of already assigned grade values.
The script responsible for UI: `source-settings/global-grading-settings/index.php`.

The pre existing values from the database are sent in a PHP array `allGlobalGradingSets` from `api/global-grading-setting.php` .

Related PHP scripts:
```
routes/api.php
GlobalGradingController.php
assets/js/globalGradingSetting.js
source-settings/global-grading-settings/index.php
api/global-grading-setting.php
```

SQL involved:
```
global_grading_sets
global_grading_set_values
```
# Symptom Type Settings

The UI is handled by `source-settings/symptom-type-and-origin.php`.
Sources are loaded in the search drop down by PHP variable `allBooksMagazines` which is generated from `api/book.php`.

For a particular source, the data in the select options are loaded by `assests/js/source-settings.js`. The script sends ajax request to the Symcom master data API with route link `source/source-setting` and is then handled by `getSourceSetting` method of `SourceController`.

Saving of the source type settings is done with `assets/js/ajaxFormSubmit.js` script.
The `content-form` class of the `form` HTML tag is identified by the script and `data-source` and `data-action` fields of this `form` tag is used to generate the route link for connection with Symcom master data API. It is then handled by `saveSourceSpecificSymptomTypeAndSymptomOriginSetting` method of `SourceController`.

Scripts:
```
source-settings/symptom-type-and-origin/index.php
assets/js/ajaxFormSubmit.js
assets/js/source-settings.js
```

SQL tables:
```
source_specific_symptom_settings
sources
```
# Grade Setting
*Displays the grades assigned to particular source.*

The UI is handled by `source-settings/font.php`.
Loading of saved data is executed by `assests/js/source-settings.js`, which sends ajax request to the Symcom master data API with route link `source/source-setting` and is then handled by `getSourceSetting` method of `SourceController`.

Saving of the source grade settings is done with `assets/js/ajaxFormSubmit.js` script.
The `content-form` class of the `form` HTML tag is identified by the script and `data-source` and `data-action` fields of this `form` tag is used to generate the route link for connection with Symcom master data API. It is then handled by `saveSourceSetting` method of `SourceController`.

Scripts involved:
```
assests/js/source-settings.js
assets/js/ajaxFormSubmit.js
source-settings/font.php
routes/api.php
SourceController.php
```

SQL table involved:
```
source_grading_settings
sources
```