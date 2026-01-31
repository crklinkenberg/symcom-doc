---
{"dg-publish":true,"permalink":"/topics/ordering-of-connected-symptoms-on-the-basis-of-their-connection-type/"}
---

#comparison 

Connected symptoms when displayed are displayed in order like: Connect Edit => Connect => Paste Edit => Paste.
  

This ordering is done in both front-end and back-end scripts. For front-end `connectionSort()` JS function is used. For backend, connected symptoms when displayed `symptom-connection-operations.php`  PHP script executes the connected symptoms ordering before returning the symptom information to the comparison page.