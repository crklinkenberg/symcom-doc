---
{"dg-publish":true,"permalink":"/topics/boenninghausen-sources/"}
---

#import 
### Background:
Bonninghausen is a special sources where symptoms are of different format in the original document. The source is not compatible for importing in the Symcom database and so `Bonnighausen` menu point  provides a platform which extracts the symptoms from Bonnighausen source and transfers the converted source and its symptoms to Symcom Master Data.

In order to import it, rubrics heading are first imported which is a document with headings and symptoms strings below it.

Example of content inside the heading import document:
```
@K:Gemüt

I. - 1. - ANGEGRIFFENHEIT ÜBERHAUPT · gemüt

Angegriffenheit.1

@K:END

I. - 1. - ANGST · Furcht · Schreckhaftigkeit · ängstlich

Angst.1

I. - 1. - BOSHAFTIGKEIT · gemein

Boshaftigkeit.2
```

Here, `@K:Gemüt` is the chapter hint. `I. - 1. - ANGEGRIFFENHEIT ÜBERHAUPT · gemüt` is the heading and from the below line `Angegriffenheit.` is the symptom with page number `1`, which is at the end of the symptom string.

Similarly, `I. - 1. - BOSHAFTIGKEIT · gemein` is the heading, the below line `Boshaftigkeit.` is the symptom string with page number `2` at the end.

Once all headings are inserted to the database, the editors copy paste contents from a document which contains many Bonnighausen headings.

Example of contents from the Bonnighausen headings:
```
@G:1

{2} bttb  I. - 1. - ANGEGRIFFENHEIT ÜBERHAUPT · gemüt  [ 124 ]

{2} bttb  I. - 1. - ANGST · Furcht · Schreckhaftigkeit · ängstlich  °  [.69 ]

{2} bttb  I. - 1. - HOFFNUNGSLOSIGKEIT · verzweifelt  °  [.46 ]

{2} bttb  I. - 1. - MISSTRAUEN · Zweifel · Argwohn  [.27 ]

{2} bttb  I. - 1. - VERDRIESSLICHKEIT · unzufrieden · mürrisch · übellaunig  [.87 ]

{2} bttb  I. - 1. - VERLIEBTHEIT · Manie  [.45 ]
```

In the import process of these contents, the input headings sent for process are matched with the already existing rubrics headings. When the matched heading is found, the symptom associated with the heading is approved. The approved symptoms can later be transferred to the Symcom Master Data under Bonnighausen source. The un-approved headings are also available for analysis after import process is compete.

### Technical Details:
#### Heading import:
The rubrics heading needed to be imported first. The UI for headings import is handled by `import-bonninghausen-rubick-headings.php` script. The contents pasted in the text box when submitted is first validated by JS function. 

Each input line is processed one by one just like the [[Topics/Source Import\|Source Import]] process but is handled by `importedStringManipulationProcessForBonninghausen()` PHP function for string manipulations. 

The imported symptoms are saved in the `bonninghausen_symptoms` SQL table. The table structure is same like the `symptoms` SQL table. Any grades associated in this process is saved in `bonninghausen_symptom_grading_settings` SQL table.

The display of imported headings and symptoms is handled by `bonninghausen-symptoms.php` script and is similar in code like the `symptoms.php` script.

The deletion of imported headings is handled by `new_customised_datatable_list_view_form` HTML id which then involves `bonninghausen-rubrics-headings-delete.php` script for deletion.

#### Bonnighausen Symptom import:
The `import-bonninghausen.php` script is the main UI for importing and transferring Bonnighausen symptoms. The headings to be imported are pasted in the text box and after submission is validated by JS function and then is processed by the same script.

Each input line is processed one by one just like the [[Topics/Source Import\|Source Import]] process but is handled by `importedStringManipulationOfBonninghausenHeading()` PHP function for string manipulations. 

The imported symptoms  after match with headings from are saved in the `	bonninghausen_approved_symptoms` SQL table. The table structure is same like the `symptoms` SQL table. Any grades associated in this process is saved in `bonninghausen_approved_symptom_grading_settings` SQL table.

The un-matched headings are inserted in `bonninghausen_re_importable_headings`.

The approved symptoms are display under `bonninghausen-approved-symptoms.php` script and is similar in code like the `symptoms.php` script.

The un-approved headings are display under `bonninghausen-un-approved-heading.php` script and is similar in code like the `symptoms.php` script.

The deletion of imported headings is handled by `new_customised_datatable_list_view_form` HTML id which then involves `bonninghausen-master-delete.php` script for deletion.

The transfer of the symptoms to Symcom Master Data is processed after click on HTML class `transfer-btn`. It is then handled by `bonninghausen-symptoms-transfer-to-main-import.php` script. The symptoms and its related gradings are selected from `bonninghausen_approved_symptoms` and `bonninghausen_approved_symptom_grading_settings` SQL tables and is then inserted to `symptoms` and `symptom_grading_settings` SQL tables.

Other related SQL table: `bonninghausen_import_settings`.
