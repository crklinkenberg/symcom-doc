---
{"dg-publish":true,"permalink":"/topics/hering-source-import/"}
---


#import 
### Technical Details:

Hering Sources are special sources with bar and pi symbols in the beginning of the string.

In some symptoms theta θ symbol which will appear at the end of the symptom string. The parts after the theta symbol including the symbol itself should not be affected by the grading process. Hering Sources will not contain different text formatting other than plain after the theta part.


For this, "symptom_theta_diagnosis" SQL table is created.

PHP functions thetaDiagnosisOperation() is used for the processing of theta parts in a symptom during the import process. This function takes the symptom string as parameter and when theta symbol is detected, it extracts the characters after it and appends a customized HTML tag named "theta-normal" before saving it in the database.

  

This "theta-normal" customized tag is also added to the conversion array in convertTheSymptom() PHP function in order to make the whole string compatible for the grading process.

  

Wildcards like `{{xoYox}}` is used for theta symbol filteration in the convertPatternPortions() PHP function.

  

NOTE: Any string manipulated in the import process must be made compatible for the grading process otherwise the program will not detect the symptom parts in order to process the grading operation. No nested tags should be present in the string which is saved in the database.

  

Function `thetaInItalics()` is used to convert theta symbol into italics in the display process.  It does not affect the values in the database.

Function `fetchThetaPart()` is used for extracting the theta parts from Hering symptom string, the input parameter is `BeschreibungFull_de` or `BeschreibungFull_en` which is present in the `quelle_import_test` i.e. symptoms table and it is of type `string`.

  

Affected scripts:
```
1. index.php
2. functions.php
3. symptoms.php
4. delete-quelle-new.php
```


  

#### NOTE:

No validation of HTML tags like `<em>, <bold>` etc and presence of special characters like `( , ), @, [, ]` in the theta symptom part for Hering sources is applied  during programming.

  

New PHP variable $multipleCharControl is added to control the double appearance of bar and pi characters inside the bracket contents.

This variable is then passed as parameters to seperateTheBrackedString() function.

```PHP
if($parOccurrence !== false)
    $BeschreibungOriginal = seperateTheBrackedString($BeschreibungOriginal, "(", ")","", $multipleCharControl);

$braOccurrence = mb_strpos ( $BeschreibungOriginal, "[" );

if($braOccurrence !== false)
    $BeschreibungOriginal = seperateTheBrackedString($BeschreibungOriginal, "[", "]", "", $multipleCharControl);

$BeschreibungOriginal = removeBlankTags($BeschreibungOriginal);
```

This passed parameters act as a flag in the seperateTheBrackedString() function. If this flag is active then operations from the function findTheOpenedTag() is prohibited.

```PHP
//A part of the code inside the seperateTheBrackedString() function.
$openedTag = findTheOpenedTag($remainingBeginingToOccurrenceString);
$prohibitOpenTag = 0;
if($multipleCharControl)
	$prohibitOpenTag = 1;
if($openedTag != "" && $prohibitOpenTag == 0){
....
....
}
```