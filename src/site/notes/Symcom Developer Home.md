---
{"dg-publish":true,"permalink":"/symcom-developer-home/","tags":["gardenEntry"]}
---

# Symcom Developer Guide
Last Update: April, 2024.
Getting Started:
Below are some important sections which help understand the Symcom Project and its work structure. 

#### **Overview**:
The site [www.reference-repertoy.com](http://www.reference-repertory.com) is the gateway to the main administrator panel. Upon logging in, addition of new books, new magazines, access to existing books, magazines, and grading configuration for fonts of sources, including details of medicines, authors, publishers, and tester (provers) can be found and edited.

The admin panel is also provided with an import section for new source import. Once logged in the user can choose to perform several actions like comparison between different sources, connection of symptoms in the comparison process: addition and modification of provers, source references, authors, synonyms etc. Additionally, there are also platforms like “materia-medica” and “history” to manage and handle the sources inside the Symcom application.

Below are some important German words and its English translation for better understanding of the full document.

| German word              | _Translated to English_ |
| ------------------------ | ----------------------- |
| 1.      Quelle           | _Source_                |
| 2.      Arznei           | _Drug_                  |
| 3.      Prüfer           | _Tester_                |
| 4.      Literaturquellen | _Literature reference_  |
| 5.      Beschreibung     | _Description_           |

For a full detailed understanding of the technical aspects, this documentation is provided with a technical guide section.

#### **Symptom Import**:
Imports of new symptoms to existing sources are done in this section. Import settings for Quelle, Arznei and Prüfer are to be filled by the user. Symptoms should be pasted from Microsoft Word document in the text editor.

Certain rules are there according to which import of symptoms is processed. The program analyses the imported symptoms and saves them according to the rules, confirmations for unrecognized patterns is also done by the program.

[[Topics/Rules relating to symptom import\|Rules relating to symptom import]]
[[Topics/Symcom Developer Guide (Work Chart)\|Symcom Developer Guide (Work Chart)]]

#### **Font Settings**:
Font settings for display of different symptoms of the Quelle (_sources_) can be done from the main menu in “Setting Sources” option. The menu contains grading values for different text formats of the symptom. The grading values are set with values like 1, 2, 3 etc. These values are assigned in “Grading” settings menu where each value represents font formats like bold, italics etc.

When for a particular source, the grade is assigned for the already defined grade values in the “Grade Setting” page, the symptoms of the source are converted whenever it is displayed.

For example: If for “Bold” option the value is assigned to number 2 in the “Gradings” section and if for a particular source the “Kursiv” option is assigned to number 2 in the “Grade Setting” page then since the number 2 is defined for “Bold’ option, the symptoms in kursiv (italics) will be converted to bold font whenever it is displayed in the Symcom application.

#### **Symptom Type Setting:**
Symptoms can be defined by a type and the symptom type of a particular source can be defined from the “Symptom Type Setting” menu option.

Symptom type can also be defined for individual symptom via the edit option for the symptoms. In this case, the individual symptom type setting will be of higher priority than its source values.

#### **Comparison**:
Comparisons among symptoms of different sources are done in this section. Initial source and comparison source are selected from the existing source list. Language of the symptoms, including percentage to compare is also selected. The comparing sources are always younger than the initial sources in the comparison process.

In the comparison page, connection functions like connect, connect-edit, paste, and paste edit can be done among the symptoms. If the editor is in doubt about the connection, the editor has the option to mark the connection as non-secure. All non-secure connections are verified by the supervisor before the final save of the comparison is done. There are also options to add comments and footnotes to the symptoms and view its information and translation.

Multiple comparing sources can be selected for a single initial source. When multiple combined sources are compared, there may be situations when the initial source may become younger or equal to the comparing source year. In such cases, the **symptoms when connected are swapped**. Functionality of symptoms for connections, connect-edit, paste, paste-edit and swap are different and follows a series rules.

[[Topics/Basic Rules relating to connection of symptoms in comparison page\|Basic Rules relating to connection of symptoms in comparison page]]
#### **Saving of Comparisons:**
Comparisons after proper inspection of non-secure connections and markings by the editor and the supervisor can be saved. Whenever a comparison is saved, connect, connect-edit and swap connections are preserved for further comparisons and editing. All initial and comparing symptoms become a single symptom list which are displayed chronologically as per their source year. All paste and paste edit connected symptoms are sorted just below its initial parent. This new combined source becomes ready for further comparisons with other sources.

_NOTE: Chronological means ascending to descending here and this sorting order is only required in the final completed comparison version. During comparison, chronological order is not shown rather the latest connection is shown first under the initials in case of combined source comparisons.

[[Contents\|Contents]] : Click to go through all the topics.