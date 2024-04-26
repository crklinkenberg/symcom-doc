---
{"dg-publish":true,"permalink":"/topics/symcom-developer-guide-work-chart/"}
---


Technical Help:
The whole project is controlled with three different versions. Below are their details:
1. Development:
	Link: http://www.dev.reference-repertory.com
	Database: development_repertory
2. Staging:
	Link: http://www.stage.reference-repertory.com
	Database: staging_repertory
3. Production:
	Link: http://www.reference-repertory.com
	Database: production_repertory

Source Import:
![Import WorkFlow.png](/img/user/assets/Import%20WorkFlow.png)
Upon submission of the import form, whole functionality of import, export and saving of symptoms according to the rules is performed by the dev-exp/index.php page.

All PHP functions can be found in dev-exp /functions.php page.

Font conversion of the symptoms are also done during the process of import, but functioning and implementation of  full font conversion is explained in the next section.

As showed in the above figure (Fig 1), the following processes takes place:

1. Submission: The user selects import settings, language, Arznei, quelle, Prüfer and pastes the symptoms from Microsoft Word document to the text editor. Upon submission, the program checks for any error with validations, if errors are found, the program shows an error in the main import page.

2. Initial Processing: The symptom text is taken as a string, cleaned and kept as an element inside an array () whenever a line break is found.
	1. The program checks if symptoms are already added to the mentioned source by searching for records in the “quelle_import_master” and “temp_ quelle_import_master” SQL tables in the database. If any errors are found in this process, the program shows error in the main page, else it continues for the next steps.
3. Pattern Identification: The array is iterated and for each element, the first and last character is taken out. The first character is crucial because this helps the program to identify different patterns(like symptom number, graduation, time, prover etc.) within the symptom text. Similarly, the last bracketed string is also processed for pattern identification.

The program also processes the symptom text strings with font configuration of the sources. Hence, cleaning, trimming and addition of new HTML tags also happens simultaneously in this step.

- The symptom text is kept in a PHP variable “Beschreibung”. Different Beschreibung versions are stored in the SQL table.
	- The field “beshurbamg_plain” stores simple text of the symptom without any text formatting or any customized HTML tag.
	- The field “beshurbang_original” contains symptom text and if the imported text has bold text format then it is converted to sperschaft (space).
	- The field “beshurbag” contains symptom text as it is from its original document.
	- The field “beshurbung_full” contains symptom text with all ending brackets.
	- The field “searchable_text” contains symptom text without the ending brackets.

- For extraction of Prüfer data from the string, the program first checks if any word starts with @P, if many  strings for Prüfer are found then all values are taken in a string and are separated by a delimiter “{#^#}”.
    
- Similar process also takes for Literaturquellen that is @L. Here “lookupLiteratureReference()” function is used for searching the processed string in the database table.
    
- For @N, which is a pattern to identify symptom number, first the program extract the strings between “( )” parenthesis and are then checked whether it is numeric or not. The final string is stored in “temp_quelle_import_test” SQL table under field “Symptomnummer”. If any mismatch is found, then the PHP flag “isSymptomNumberMismatch” is used for approval from the user at the end of Submission.
    
- Other patterns with “ @ ” in the beginning of string  and their respective meanings are mentioned below.
    @A:Remedy
    @AT:Similar remedy, Similar symptom text (e.g. Opi., during the day)
    @TA:Similar symptom text, Similar remedy (e.g. small boils in crops, Sulph.)
    @L:No Author, Aepli sen. in Hufeland Journ. YYV. (when there is no author reference) @U:Unclear(Unklarheit) @F:Footnote(Fußnote) @T:Text/Symptom text @Z:Time @K:Chapter (Kapitel) @UK:Subchapter @UUK:Sub Subchapter @S:Page  @C:Comment(Kommentar) @V:Hint(Verweiss) @G:Grading/Classification(Graduierung)
    All the extracted values from the patterns mentioned above are stored in “temp_quelle_import_test” SQL table in their respective fields.
    
- The symptom-pruefer relationship is stored inside “temp_symptom_pruefer” table.
- The pruefer details is stored in “temp_pruefer” table.
- If no approval for pruefer is required then it is stored in “temp_approved_pruefer” table.
- Remedy is stored in “temp_remedy” table.
- “Symptom and literature reference” relationship is stored in “temp_symptom_reference” table.
- The literature reference details is stored in “temp_reference” table.
- If no approval for literature reference is required then it is stored in “temp_approved_reference” table.
- Need for approval is searched in “temp_quelle_import_test” table, if no approval is needed then following steps takes place, else redirected to main page for asking questions.
	- Insertion takes place from “temp_quelle_import_master” to “quelle_import_master”.
	- Relationship betweeen  arznei and quelle is stored in “arznei_quelle” table.
	- Insertion of symptom text takes place in “quelle_import_test” from “test_quelle_import_test”.
	- Relationship between symptom-pruefer is stored in “symptom_pruefer” table.
	- Relationship between symptom-reference is stored in “symptom_reference” table.
	- Pruefer, remedy and reference values are finally stored to pruefer, remedy, reference tables from their temporary tables.
- First checks for approval of any pre defined tags like @P, @L, @K etc.
- Then checks for priority of pruefer, remedy, part of symptom, symptom edit, etc.
- According to the rules, the program asks questions for each of the categories based on priority in a pop-up. This pop up contains an HTML form which sends the user input to PHP pages with prefix “approve” in the file name, like: approve-as-pruefer.php.
- The pop up will continue appearing, till user approves it with yes, no or DO(direct order) button. The DO(direct order) helps the user to manually select the category in which the unidentified pattern belong.
	After successful insertion, data from temporary tables are deleted.
- Bücher: contains details of all the sources. Addition of new source can also be done here.
    Related SQL tables:
	- quelle: stores all quelle data including herkunft_id, verlag_id. Here, the field quelle_type_id=1.
	- quelle_pruefer:stores pruefer relating to that quelle.
	- quelle_autor:stores author relating to that quelle.
	- quelle_grading_settings:grading setting of that quelle for font display.
- Zeitschriften: contains details of all the sources but sources are categorized as magazines.
    Related SQL tables: same as previous but in quelle table, the field quelle_type_id = 2.
- Arzneien: details of all the arznei.
    Related SQL tables:
	- arznei: stores all arznei data.
	- arznei_autor: relationship between arznei and autor.
	- arznei_quelle: relationship between arznei and quelle.
- Autoren: details of all the authors.
    Related SQL tables: autor: stores all author data.
- Prüfer: details of all the proofers.
    Related SQL tables: pruefer.
- Herkunft: details of origin.
    Related SQL tables: herkunft.
- Verlage: details of publishers.
    Related SQL tables: verlage.
- Literatur: details of literature.
    Related SQL tables: reference.
- Grade Schriftarten: This is the global grading setting menu. Here different text formats like Normal, Sperrschrift, Kursiv Sperrschrift etc are given unique values like 1,2,3,etc.
    Related SQL tables:
	- global_grading_sets: stores value whether settings is for font or colored.
	- global_grading_settings: stores the values for different font formats like normal, kursiv, bold etc.
	- global_grading_set_values: contains IDs of all font formats.
- Setting (Font Conversion): This setting menu has select option for different customized tag names with values 1,2,3 etc.
    A source can be configured with a font setting and this font configuration is effective when symptoms are displayed under that source. Full steps of font conversion are shown below:
	The “lookupPruefer()” function, searches for the processed Prüfer in the database tables. If values for Prüfer are not found, then a PHP flag is used, which is then used later for approval of the pattern from the user. According to the rules a priority value is also set which helps the program to identify the string and ask questions regarding its approval from the user.
	
	The final values for Prüfer is stored in an associative array for further use in the program.

4. Storing in temporary tables: The data from the symptom text including pattern approval request and  priorities are all stored in an associative array and is then inserted into “temp_quelle_import_test” SQL table.
    
    Approval for unidentified patterns: When approval is required for strings inside barckets at the end of the symptom text or when no records of prufer, reference etc is found then the page is reloaded with a GET parameter “master”. This helps in identification of the source from “temp_quelle_import_test” table. The program:
    
    Final processing: In this step, final insertion of the symptom in “quelle_import_test” takes place and all categories of the symptom text like pruefer, remedy, refernce, date, etc are stored in different fields of the table.
    
    Admin panel: Handling of all Symcom data can be done in this admin panel. This main dashboard consist of:
    
1. Vergleich: which is a link to the source comparison page.
2. Stammdaten: this option handles all the data.
3. Benutzer: list of users.
4. Import: which is a link to the import page.
Stammdaten:   This menu has different option for handling of data stored in the SQL databases.
1. Symptom is imported, the user clicks submit and the program starts processing the symptom text.
2. The program searches for patterns by checking the first and last charcter in a string. It also detects other characters like °(degree) or *(asterisk).
3. Detected patterns are passed to different font formatting functions which returns the string with encapsulated customized HTML tags.
4. The symptom text is saved in the database.
5. Setting menu in the admin panel has grading values for all the customized tags like “parentheses-normal”,” asterisk-grossbold”,” non-asterisk-degree-bold” etc for each source.
    
    Now, if the global grading setting , value for text format “Bold” is given as “3" and if in the settings menu, “asterisk-grossbold” option is set with value “3”, then when the symptom is displayed for that source, if the symptom text contains words with tags “asterisk-grossbold” that is `< asterisk-grossbold >someword</ asterisk-grossbold >` then due to global grading font setting, the tags will be converted and the word will be displayed in bold.
    
6. All customized tags are first converted to HTML tags like `<em>,<strong>`  when the program first cleanses the symptom text during the import process, if the source has grading settings configured then only conversion of the tags according to the font settings occurs otherwise not.
    
    Related SQL tables:
	Example: If strings like *some word is detected then the program identifies it to be a bold word with asterisk, hence, it converts the string into `<asterisk-bold>some word</asterisk-bold>`.
	- quelle_grading_settings: Settings for all custom HTML tags for particluar sources is stored here.
	- symptom_grading_settings: Settings for all custom HTML tags for particluar symptoms is stored here.

---

**Comparison:**
Whole process of comparison can be divided into three steps:
1. Comparison between quelle(sources).
2. Connections among quelle, that is connect, paste, connect-edit, paste-edit.
3. Saving of the comparison sources.
4. Comparison among quelle:
    For every comparison, an SQL table is created using the user setting like arznei and language. The whole comparison is done in 0% and stored in the database.
    
    Work Flow is mentioned in the below figure.
![comparison.jpg](/img/user/assets/comparison.jpg)
    Fig 2: Work Flow showing comparing source process.
As showed in the above figure (Fig 2), the following processes takes place:
- Comparison Button Click: The user selects the settings for comparison. This setting include:
	1. The percentage(cut-off) in which the comparison would be done.
	2. The language for the sources, that is German or English.
	3. Comparison option: compare only symptoms or compare whole symptom text(where last string words with brackets will also be considered).
	4. Arznei selection.
	5. Initial source: according to arznei, initial sources will be displayed in the select box.
	6. Comparison source: according to arznei, comparing sources will be displayed in the select box.

- Initial processing: The compare setting submitted is processed by the program with the help of an id “symptom_comparison_form” and below steps are processed:
	1. Form validations are done, if no errors are found then an ajax request is sent to “check-if-comparison-table-exist.php” page. This page stores all the setting fields in an PHP SESSION variable with name “comparison_table_data”.
    
	    This SESSION variable also stores:
	- Comparison table name as:
		"comparison_table_arzneiID_initialSourceID_comparingSourceIDs_language”
		
    In above, the words in bold are the values taken from comparison setting menu.
    
NOTE: Two more tables are created during comparison. These tables are:
Same name as comparison table with suffix “_connections” added in one and suffix “_highest_matches” added in another.
The “connections” table saves the connection done for that particular comparison and the “highest_matches” table stores the highest matched percentages of all the symptoms. The “highest_matches” table is later used for displaying the unmatched symptoms.

The program searches for the comparison table in SQL table “pre_comparison_master_data”. Steps taken when table found or not found is shown in next sections.
- Create comparison table: When comparison table name is not found in the SQL table “pre_comparison_master_data”.
	- The program first makes an entry with the comparison table name in the “pre_comparison_master_data” SQL table for keeping a reference of the comparison table.
	- Using shell commands, the creation of comparison table is executed in “create-dynamic-comparison-table.php” page.
	- Whilst the comparing table creation with the user’s settings is executing, the “pre_comparison_master_data” SQL table is updated with a status “processing”, and while the table creation process is still continuing, the user will be displayed a pop-up showing “the creation process is still executing in background”.
	- The program checks the table status in fixed intervals, if execution is still processing then, the user will be displayed the pop up, if status is “complete” then next step follows.
    
- Create comparison table: When comparison table name is found in the SQL table “pre_comparison_master_data”.
    Fetching of Data Starts: When a user submits settings to compare between sources, and if comparison table is found in the “pre_comparison_master_data” with status “complete” then:
	-  The comparison page is reloaded.
	- Comparison table name is retrieved from the SESSION variable “comparison_table_data”. The number of initial symptoms to be displayed per page is also taken.
	- The comparison table name is searched in the database and according to the percentage set by the user, the symptoms from initial sources(in green color) and comparison sources is displayed in rows.
- Creation of connection and highest matches tables: Highest matches table and connection table are created at the same time when comparison table creation process starts. The “connection” table is by default empty for single source comparisons and the highest match table contains all the symptoms with its highest percentage match.