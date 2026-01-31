---
{"dg-publish":true,"permalink":"/topics/import-section-additional-concepts-allen-synonym/"}
---

#import
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
