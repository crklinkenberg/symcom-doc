---
{"dg-publish":true,"permalink":"/topics/symptom-type-setting/"}
---

#general 

Symptom Type Setting from Menu Point helps assign symptom properties to a particular source.

Any of these options can be assigned to any particular field.

![Pasted image 20240423163941.png](/img/user/assets/Pasted%20image%2020240423163941.png)

  
For symptom origins, the options that can be assigned are:

![Pasted image 20240423163952.png](/img/user/assets/Pasted%20image%2020240423163952.png)

Technical Details:
1. The UI is controlled by `symptom-type-and-origin.php` script located under directory `source-settings`. The population of sources is done by `api/book.php` inside this script.
2. PHP variables `symptomTypeOptions` fetches saved data for symptom type HTML form with id `symptom_types`.
3. When the HTML form is saved, it is handled by the Laravel `SourceController`. The method responsible for this operation is `saveSourceSpecificSymptomTypeAndSymptomOriginSetting()`.
4. Model associated: `SourceSpecificSymptomSetting`.

