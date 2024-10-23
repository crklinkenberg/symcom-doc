---
{"dg-publish":true,"permalink":"/topics/symcom-master-data-guide-api-included/"}
---


Technical Details:
Master data includes data of Symcom Master data menu topics: Books, Magazines, Medicines, Authors, Testers, Source Origins, Synonyms, Publishers and Literatures.

For each of these topics CRUD operations can be performed. 
The backend is controlled by Laravel API. 
Here is the link to Symcom Master Data API Guide.: https://documenter.getpostman.com/view/15213161/2sAY4rEQ4G

Individual controllers exists for each of the topics. Backend files associated:
```
routes/api.php
Controllers/Api/UserController.php
Controllers/Api/RoleController.php
Controllers/Api/PublisherController.php
Controllers/Api/SourceOriginController.php
Controllers/Api/AuthorController.php
Controllers/Api/TesterController.php
Controllers/Api/SourceController.php
Controllers/Api/MedicineController.php
Controllers/Api/LiteratureController.php
Controllers/Api/GlobalGradingController.php
Controllers/Api/SynonymLiteratureController.php
Controllers/Api/SynonymController.php
```
 
 The UI is controlled by individual files present inside directories `master-data/`and `api/`.

Frontend Validations are being controlled by:
```
assets/js/ajaxFormSubmit.js
assets/js/formValidation.js
assets/js/common.js
```

Any data existing under master data can later be used in the import process and thereby is related to the comparison processes.


