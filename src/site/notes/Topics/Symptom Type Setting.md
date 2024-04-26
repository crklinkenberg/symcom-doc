---
{"dg-publish":true,"permalink":"/topics/symptom-type-setting/"}
---


Symptom Type Setting from Menu Point helps assign symptom properties to a particular source.

Any of these options can be assigned to any particular field.

![Pasted image 20240423163941.png](/img/user/assets/Pasted%20image%2020240423163941.png)

  
For symptom origins, the options that can be assigned are:

![Pasted image 20240423163952.png](/img/user/assets/Pasted%20image%2020240423163952.png)

Technical Details:

1. "source-settings/quelle-settings/index-symptom-type.php" is the form page where input is done with the help of "quelleSettings.js" script.
    
2. The form data are controlled by the "QuelleController.php" script. The function involved is "saveQuelleSymptomTypeSettings()".
    
3. The data taken are saved in the "quelle_symptom_settings" sql table in the database.