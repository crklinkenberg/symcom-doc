---
{"dg-publish":true,"permalink":"/topics/sorting-of-symptoms-based-on-superscript-numbers/"}
---

#general 

Sorting the symptoms according to the superscript (exponent) at the end of each symptom of a word file. After sorting, preprocessing of the symptoms in Word will be done. Only then it is added to `SymCom`.

### **Some specifics**

If there are several numbers in a row, the first number must always be used, no matter if there are any brackets or the slash-sign.

Examples:

```
Allgemein Affektionen der linken Seite des Kopfes.327/88  → 327

16/1 → 16

Vor Tisch wenig Appetit.[34]25/15 → 34

[347]432/32 → 347

Er hatte sich beim Heben eines schweren Gewichtes überanstrengt **||**.[135]184 → 135

Seit 10 Monaten kein Rückfall.[Marweg]480/10  → 480

Nach einer Woche machte sie noch eine psychische Krise durch wegen des verlorenen Kindes, die aber spontan wieder verging.[Fuckert]127(2/96)  → 127
```

All these number combinations are always **_one_** character and only the **_first number_** in the row **_is relevant for sorting_**.

### **Special exceptions**
There might be also a character at the end (seen this only once):
```
Nach der 1. Gabe _Ruta_ 200 war der Schmerz verschwunden.[7]219H   → 7
```

It might happen, that the number at the end is missing:
```
Baker-Zyste (_Calc-p_. [chronisch]).Hershoff
```

This symptom should then be listed at the end or beginning.

Numbers in the symptoms are ignored:
```
FURCHT*;1 in engen Räumen, Klaustrophobie*.286  → 286
```

### Technical Details:
Can be accessed: http://www.dev.reference-repertory.com/dev-exp/sort-symptoms-to-file.php
`CKEditor` is used using CDN.

The form in the web page accepts option for both sorting with number and sorting with letters. At present only sorting with number is enabled and programmed.

Any superscript content not containing any number will be sorted at the end of the list. Other symptoms with number in the superscripts are ordered as per the rules mentioned above.

`supContentControl()` PHP function controls the identification the superscript contents and extract the digits present in the superscript content. If the superscript content is no number then digit 10000 is returned by the function.

The digits returned are then sent to `insertionInMasterArr(master_array, digits_extracted, paragraph_content )` PHP function which does insertion in `master_array` with `digits_extracted` as key and `paragraph_content` as value. Conflicting keys are also handled by this function.

Once, the `master_array` is formed, each of the values are written to a `.docx` file using `PHPWord` and sent to the user.



