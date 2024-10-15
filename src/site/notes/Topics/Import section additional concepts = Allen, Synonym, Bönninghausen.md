---
{"dg-publish":true,"permalink":"/topics/import-section-additional-concepts-allen-synonym-boenninghausen/"}
---

## **Concept as on date: Feb 18, 2023.**
# Allen source Literatur/reference detection concept

Allen sources are special kinds of sources where literatur/references are kept in the document in a different manner, which the program needs to understand and detect them and needs to assign the reference with the associated symptoms. Here is the example of a Allen source:

```
Literatur start
1, Hahnemann, in Chr. Kn., S. Hahnemann, 1839.
53, Fr. Hahnemann, in Chr. Kn., S. Hahnemann, 1839.
22b, Nenning, in Chr. Kn., S. Hahnemann, 1839.
4, Wahle, in Chr. Kn., S. Hahnemann, 1839.
18a, Walther, in Chr. Kn., S. Hahnemann, 1839.
34, Ardoynus, de venen, Lib. II, C. XV (statement, -Hughes), in Chr. Kn., S. Hahnemann, 1839.
7, Hufel. Journ. (statement, -Hughes), in Chr. Kn., S. Hahnemann, 1839.
8, Morgagni, de sed. et Caus. Mort. (observation, -Hughes), in Chr. Kn., S. Hahnemann, 1839.
Literatur end

Agitation, with the sore throat, [53].
An indolent excitement, almost as after coffee, [1].
She talks nonsense day and night, [4].
Irritated cross temper (eighth day), [22b].
Headache (ninth day), [18a]; (second day), [34], etc.
Disturbance in the head, so that she thought she had lost her reason, [8]. [Revised by Hughes.]
```

In the above Allen source example the first paragraph contains only the literatur/references information. Here in the first paragraph we have two identifier text “Literatur start” and “Literatur end” for identifying the starting and ending of the literatur/references information section. In the Allen source document the strings after the identifier “Literatur end” are considered as symptom strings.
The literatur/reference identifying number which is found in the symptom string, is presented as a superscript number in the original version and the converted version of the symptom string. I.e.:


| Imported symptom                                            | Original symptom                                          | Converted symptom                                         |
| ----------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| He believes he will not be able to recover his health, [4]. | He believes he will not be able to recover his health, 4. | He believes he will not be able to recover his health, 4. |

# Synonym concept

We have synonym database or synonym section in our main administrative panel as Synonyms main menu and two submenus synonym DE and  synonym EN .

Here we store and manage all the synonyms of their respective languages, we can add new and modify existing synonyms.

Now when we import a source it collects all the synonyms from the synonym database of the importing source language. In the import process for each symptom the program finds/match the similar word from the symptom string and the synonym database data. And the program links the matched word in the symptom string with synonym words that are matched and stores the information in the symptom string row. We can see these matched synonym information in the info popup box of the symptom string in comparison mask.

When we compare two sources these linked synonyms are also used in the comparison. When two symptom strings gets compared these associated synonym words also participate in the comparison process.

We can also add a synonym after importing a source. We need to open the symptom view link of that source and there we will find a Add synonym column for each symptom string with “+” icon button, clicking on this plus icon opens up a popup to add a new synonym for that symptom. And this way also we can add a synonym. i.e.:

![Pasted image 20241015124904.png](/img/user/assets/Pasted%20image%2020241015124904.png)

![Pasted image 20241015124911.png](/img/user/assets/Pasted%20image%2020241015124911.png)

When there is a source which is already imported, and after importing a source we add new synonyms. In this scenario we get an “update” button activated in the materia medica page synonym column with all sources rows which need to be updated with the latest synonym database.

![Pasted image 20241015124921.png](/img/user/assets/Pasted%20image%2020241015124921.png)

Clicking on the “update” button/link of the synonym column(as shown in above screenshot) of a particular source, on the successful completion of the update process that particular source gets updated with the latest synonym database.       

We can not use a source or program will not allow a source to make any comparison with any other sources if that particular is not updated with the latest synonym database.

# @G: (Grading) concept

When we import a source in the import page, there are several elements which gets detected  and identified as elements which has certain meanings in the application and need to get process accordingly.

Here @G is one of the elements which has a certain meaning in the program. @G signifies the grading of a symptom, we can set gradings for a symptom or group of symptoms in the import process by providing @G sign just above the symptoms with the grading value. i.e.

```
@G:2

Beim Mittagsessen plötzlicher Schwindel, als sollte er vorwärts fallen [Gß.]

Beim Gehen schwindlich [Archiv f. d. homöop. Heilk. V. III.]

@G:END

Schwindel in der Stirn, besonders beim Gehen, wo es ihr ist, als ginge alles mit ihr im Kreise herum und wollte mit ihr umfallen [A.f.d.H.]

Schwindel; wenn sie sitzt und den Kopf vorwärts hält, fast unmerklich; wenn sie aber den Kopf aufrichtet oder bewegt, sogleich Gefühl, als ginge alles mit ihr herum [A.f.d.H.]

@G:3

Schwindel.
```

In the above example the first two symptoms are assigned with the grading value 2 and with the sign @G:END we are turning off the effect of the @G sign.

The symptoms which has gradings will get converted to their according fonts/formats which are set by the admin.

# @K: (Chapter) concept

@K represents chapter. Same as above @G sign @K sign also has special meaning, When we have @K sign with a value(as chapter) the following symptoms underneath the @K sign will get associated with that value(chapter) until the turn off sign of the @K sign which is @K:END. i.e.

```
@K:Kopf

Beim Mittagsessen plötzlicher Schwindel, als sollte er vorwärts fallen [Gß.]

Beim Gehen schwindlich [Archiv f. d. homöop. Heilk. V. III.]

@K:END

Schwindel in der Stirn, besonders beim Gehen, wo es ihr ist, als ginge alles mit ihr im Kreise herum und wollte mit ihr umfallen [A.f.d.H.]

Schwindel; wenn sie sitzt und den Kopf vorwärts hält, fast unmerklich; wenn sie aber den Kopf aufrichtet oder bewegt, sogleich Gefühl, als ginge alles mit ihr herum [A.f.d.H.]

@K:Kopf2

Schwindel.
```

# Bönninghausen Concept

In this concept we have special kind of source, where the source document content is different from our usual source document content. An example of Bönninghausen source document content:

```
@G:4

{5} bttb  I. - 1. - WECHSELNDE STIMMUNG · launenhaft · schwankend  °  [.41 ]

Wechselnde Stimmung.21

{5} bttb  II. - 1. INNERER KOPF - HALBSEITIG ¦ einseitig  °  [ 119 ]

@K:Kopf, innerer

Halbseitig.11

{4} ++bttb+P  VI. - 3. amel - VON SCHLINGEN · Schlucken  °°  [.47 ]

{5} bttb  I. - 1. - WECHSELNDE STIMMUNG · launenhaft · schwankend  °  [.41 ]

{5} bttb  II. - 5. OHREN - AEUSSERES OHR · äusseres  °  [.91 ]

Aeusseres Ohr.25

{5} bttb  II. - 20. AFTER - MITTELFLEISCH · Damm · Perineum  °  [.37 ]

Mittelfleisch.

{5} bttb  II. - 27. SCHNUPFEN - NASENABSONDERUNG - SCHARF · beissend · wundmachend  °  [.45 ]

{4} bttb  II. - 10. ZÄHNE - OBERZÄHNE · oben  °  [.71 ]
```

Here in above example few strings are heading string i.e. 

`“{5} bttb  I. - 1. - WECHSELNDE STIMMUNG · launenhaft · schwankend  °  [.41 ]”` and few strings are symptoms string i.e.  `“Wechselnde Stimmung.21”`. These symptom strings are created by human from the heading string.

So, in our Bönninghausen source document we generally have one heading string and just below that a symptom string created from that above symptom string.

Sometimes we only have bunch of heading string and no symptom string for those heading strings, in this scenario we consider these heading strings as bad symptoms.

**Bönninghausen import process explanation**

To import a Bönninghausen source we go the Bönninghausen page by clicking on the Bönninghausen menu item from the left side menu bar of our application.

Here in this page, we select the Arznei/Remedy and Language for the import process and then copy the Bönninghausen source document content and paste it in the text editor for import. After that we click on the Submit button to import the source. After the source getting imported successfully, we get the source information/data listed in the below table on the same page. i.e.

![Pasted image 20241015125154.png](/img/user/assets/Pasted%20image%2020241015125154.png)

Here in the imported source information row, we get delete option, to delete a imported source we have to check the check box of that source in the first column of the table and have click on the dustbin icon provided on the table heading row first column and then have to follow the instruction.

We can view the imported good symptoms or we can say approved symptoms of that source by clicking the “Approved Symptoms” link provided in the 8th column of the table.

We can also view the bad symptoms (which needs to get prepared by human aging for re-importing) by clicking the “Bad Symptoms” link provided in the 9th column of the table.

In this same 9th column of the table, we also have two icon buttons download and delete.

The first icon button “download” by clicking this icon we can download the existing bad symptoms in word document to work with these bad symptoms and prepare for re-importing.

The second icon button “delete” by clicking this icon we can delete the existing bad symptoms. Purpose of this delete icon button is to provide option to the user to delete the existing bad symptoms after downloading the bad symptoms and re-importing them correctly.   

**Process of re-importing a source**

To re-import a source after correcting or organizing the bad symptoms we will follow the same import process and the newly imported approved symptoms and bad symptoms will get added in the existing of them.

To import the same source aging with the new content, we select the same Arznei/Remedy and same Language and copy the symptoms from our prepared word document and paste it in the text editor and then we click the submit button.

After successfully re-importing the new content in the previously imported source the newly analyzed approved symptoms and bad symptoms by the program gets added in their existing respective list at the end.