---
{"dg-publish":true,"permalink":"/topics/user-view-page/"}
---

#userview

Comparisons worked upon and when finished can be sent for viewing purpose to the public / users. The supervisor in the Symcom website has the privilege to send the final version of the comparison from the materia medica page to the reference materia medica (RMM) page which is basically the materia medica for the users in the user view section.

This user view section is isolated from our working database and is separate also in terms of file structure.

Current development database name: alegra_new_repertory_user_final_view.

Current staging database name: alegra_new_repertory_user_view_stage.

NOTE: At present, the user view page is being designed only for demonstartaion purpose and to test the functionalities. Full layout design and functionality will be done later.

File Structure: User Section files are controlled by the “user-view” directory in the “dev-exp” directory.

The “user-includes” directory inside it has scripts which controls the database configuration, routes, JavaScript and PHP functions.

The “middle-scripts” directory controls the overall process of each menu points, acts as a controller.

The views are all present inside the “user-views” directory.

The fetching of information of all the symptoms are done via an api and the scripts relating to it are present inside the “api” folder.

  
Important: Steps to follow to make a final compared source visible in user view:
 1. At present, developers make the finalized source available in the user view section, so the full process is not automatic, below steps should be followed. Development and staging user view sections are both independent of each other so steps should be followed in both environment whenever required.
 2. The finalized source should be checked under RMM column in the materia medica. This will copy the completed and connections table of the finalized source in the user view database.
 3. Navigate to "dev-exp/table-control-in-user-view.php" in the browser. This will update the user view database with latest data from the current active database. All database dependencies for user view section is done by this script. For migration "user-view/user-migration.php" script is used.
 4. The quelle_id of the finalized compared source is copied from pre_comparison_master_data sql table and is pasted in the quelle_id column of the user_settings sql table inside the user view database.
 5. The quelle id is pasted in the "user-view/index.php" page and is pushed.
 6. The final compared source will now be now visible in the user view section.

Below are the filtration functionalities of the user view menu points with both conceptual and technical details:

Technical Help: The “index.php” script is responsible for showing all the symptoms with customized filtration. All menu points flags are handled here, and respective functions are called for fetching and modifying the data or displaying. The final execution before display is done by the “symptom-list.php” script which is inside the “user-views” directory.

  

1. Show Source:

For each source, an abbreviation system with author and source key is designed.
![Pasted image 20240423161606.png](/img/user/assets/Pasted%20image%2020240423161606.png)
Related PHP function:

- fetchSourceViewSetting(source view flag, user id, quelle id).
    
- getQuelleAbbreviation(original quelle id, source view fetched).
    

 Database field : “source_view” in the `user_settings` MySQL table.

  

2. Show symptom type:

Under Settings Sources we have the submenu Symptom type setting.

Here we can deposit certain symptom types to the symptoms of the source.

In the default setting, the symptom types are not shown. Users can display the type of symptom behind the symptom. Default is:
![Pasted image 20240423161632.png](/img/user/assets/Pasted%20image%2020240423161632.png)

Users should be able to display the type of symptom behind the symptom:

Checking the box causes the selected symptom types to be displayed with a subscript at the end of the symptom (p, t, c and s):

  

Ex.: checking the two boxes clinical + intracurative symptoms:

![Pasted image 20240423161645.png](/img/user/assets/Pasted%20image%2020240423161645.png)

In the user page:

Pressure in the eyes.                                     

Retinal detachment.

Visual impairment. c       

Stitches in the eyes. s

Related PHP functions: fetchSymptomTypeSetting(symptom type flag, user id, quelle id).

Database field : “symptom_type” in the `user_settings` MySQL table.

  

3. Show contents in brackets:

![Pasted image 20240423161658.png](/img/user/assets/Pasted%20image%2020240423161658.png)

In the standard version, the contents in brackets that belong to the symptom text and the drug references are displayed. All other bracket contents are not displayed. By clicking the respective boxes, the user can display additional content in brackets.

![Pasted image 20240423161708.png](/img/user/assets/Pasted%20image%2020240423161708.png)

Contens in brackets input values are taken from the html form in “show-bracket-contents.php” script and then are saved in the “contents_in_brackets” field of the “user_settings” SQL table in a serialized PHP array form.

  

Related PHP functions:

  

- fetchTesterInfo(original qulle id, symptom id).
    
- fetchDrugReference(symptom id).
    
- fetchLiteratureRef(symptom id).
    
- fetchBracketContentSetting(contents in bracket flag, user id, quelle id).
    

  

NOTE: For bracket contents, at present the “searchable_text_de” and “searchable_text_en” from completed SQL table is used to display the results. When any of the options are selected, the contents are fetched using PHP functions and appended at the end of the strings with the brackets.

  

  

4. View of grades:

![Pasted image 20240423161737.png](/img/user/assets/Pasted%20image%2020240423161737.png)

All grades are activated by default. Unchecking means that symptoms with these grades are not displayed. Example: If the user only wants to see symptoms in the 4th and 5th grade, he deactivates the first four grades. If the 1st grade is deactivated, all symptoms in the 1st grade are not displayed. If no grade is activated, you will ­not see any symptoms. Doubtful symptoms (grade 0) are placed in brackets.
![Pasted image 20240423161751.png](/img/user/assets/Pasted%20image%2020240423161751.png)

The grade value for each grades are taken from the HTML form in the “show-grades.php” script. It is then stored in the “show_grades” field of the “user_setting” SQL table in a serialized PHP array form.

  

This array is fetched using the “fetchGradesSetting()” PHP function and according to the key-value pair, the grade values (1 ,2 , 2.5, 3, 3.2 etc) are then inserted into the “$gradeFilterArray[]” PHP array. This array is sent to the “convertTheSymptomWithGradingFilters()” PHP function which does all the filtration and creates the final symptom string and finally displays it.

  

  

5. Graphical Presentation:

![Pasted image 20240423161804.png](/img/user/assets/Pasted%20image%2020240423161804.png)

In this menu, users can display the symptom grades in the standard ­setting or in colour. The radio ­buttons are mutually exclusive, i.e. as soon as "Color" is activated, "Standard" is deactivated.

![Pasted image 20240423161818.png](/img/user/assets/Pasted%20image%2020240423161818.png)
![Pasted image 20240423161824.png](/img/user/assets/Pasted%20image%2020240423161824.png)


The graphical representation is taken from the HTML form in the “show-graphical-presentation.php” script. It is then stored in the “symptom_color” field of the “user_setting” SQL table.

  

This value is then fetched by the PHP function “fetchGraphicalPresentationSetting()” and the return value is stored in the “$symptomColorActive” PHP variable.

  

This variable is then sent to “convertTheSymptomWithGradingFilters()” PHP function as a parameter and this grade conversion function shows the final output.


6. Author Selection:

![Pasted image 20240423161842.png](/img/user/assets/Pasted%20image%2020240423161842.png)

By default all authors of the RMM are listed and check-marked. Users can exclude a particular author (all sources of that author) from display:

  

The user can selectively exclude individual authors by deactivating the corresponding buttons. If an author is deactivated, all sources of this author and corresponding symptoms of this sources are hidden. It is a function that can be switched on and off, the user can switch the author on again with one click and thus display his sources back in the RMM.

  

 Example: Exclusion of the author Hering, CJ and all of his works:

![Pasted image 20240423161913.png](/img/user/assets/Pasted%20image%2020240423161913.png)

Attention : If an author is hidden, not only the initial symptoms of his sources are hidden, but also all symptoms that are related to these initial ­symptoms via connect or connect edit.

  

Technical Help:

All authors are displayed using the “exclude-author.php” script in the alphabetical order. On unchecking an author, the author id is taken and kept in a JavaScript array from the “author-control.js” script and when the setting is saved, this array is converted to string and is then submitted. After which the excluded author value is saved in the “author_exclude” field in the “user_settings” SQL table.

  

Values from the SQL table is fetched using the “fetchExcludedAuthors()” PHP function and return value is exploded and is the author id is matched with each of the symptoms in the display process and accordingly the matched symptoms are excluded from the display list.

7. Time Epoch:
![Pasted image 20240423161945.png](/img/user/assets/Pasted%20image%2020240423161945.png)

Users can choose sources of a certain period of time (i.e. from beginning to 1900):

  

In this module, the user can choose the period which he wants to be displayed sources from. In the first field (Select) is the year of the oldest source 1811, in the second field is 2023; these year specifications can be overwritten.  Example: If the user only wants to display sources up to 1980, he writes 1980 in the second field. If he wants to see all symptoms from 1950 onwards, he writes 1950 in the first field and 2023 in the second field.

![Pasted image 20240423162002.png](/img/user/assets/Pasted%20image%2020240423162002.png)

The time epoch is taken from the HTML form in the “time-epoch.php” script. It is then stored in the “time_range” field of the “user_setting” SQL table.

  

This value is then fetched using “fetchTimeEpochSetting()” PHP function, the returned value is taken in an array with key “time_epoch” and is then sent along with the “quelle id” to the api for showing all symptoms. In the api function, the time range is extracted from the “time_epoch” value sent and “quelle_jahr” field of the completed table is controlled in order to produce the final lisrt of symptoms.