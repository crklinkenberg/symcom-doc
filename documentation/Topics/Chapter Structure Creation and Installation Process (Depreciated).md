Chapter Structure Document Reformatting for automatic chapter creation process:

1. The chapter structure from word document is copied and pasted in normal text file or md file. Any extra spaces are removed and space from word document format are also removed.

2. All main-head names should start with “#” symbol.

3.  All sub-sub-head names should start with “^^” symbol.

4. All headings should contain “$$$” between the English and German head words.

  

  

Steps to follow for chapter installation:

1. Open the script “chapter-installation.php”.

2. In the text field paste the formatted texts. On successful submission this script will insert chapter heads in the “chapter_main_head”, “chapter_sub_head” and “chapter_sub_sub_head” SQL tables.

3. After this open the script “chapter-structure-implant.php”, this script will save the chapter heads in English, German and also its abbreviation in separate PHP files in serialized array format.

4. Three more script “chapter-structure-de-for-use.php”, “chapter-structure-en-for-use.php” and “chapter-structure-abbr-for-use.php” should be included in whenever chapter structure is needed to be fetched in the webpage. The abbreviations are used to store the chapter head values in the MySQL table.

  

  

Chapter Head Saving in Database:

The completed table of a particular arznei contains a field with name “chapter”. This contains the chapter head name which are assigned in the chapter assigned process.

The abbreviations of chapter names are saved in the SQL table. All chapter abbreviations in each chapter weights are separated with delimiter “##&##”. .

Illustration:

Primary Weight Chapter Abbreviation ##&## Primary More Weight Chapter Abbreviations ##&## Secondary Weight Chapter Abbreviation ##&## Tertiary Weight Chapter Abbreviation

  

  

Non secure chapter

“ns_chapter_comment” and “ns_chapter” are two fields in the completed sql table which are used for marking non secure chapter assigned.

  

Chapter Structure Modifying and Deletion (Technical):

The chapter structure in the program exists in three main scripts:

- chapter-structure-en.php
    
- chapter-structure-de.php
    
- chapter-structure-abbr.php
    

These scripts are called by different webpages and the structure is shown in the program.

  

For modifying and manipulating the chapter position below details are important:

Chapter is installed only once in the program but can be implanted with modification again and again. Once, chapter is installed and working, new chapter can be added with the help of “new-chapter-assignment.php” script.

This script can add chapter, sub chapter or a sub sub chapter. Insertion is done in the database. Three sql tables are affected:

- Insertion of main chapter => chapter_main_head
    
- Insertion of sub chapter => chapter_sub_head
    
- Insertion of sub sub chapter => chapter_sub_sub_head
    

This script insert the new record in the last row of the table.

For implanting the chapter structure with new chapters “chapter-structure-re-implant.php” script under “additions” directory can be used.

  

For implanting the chapter structure with the structure and position modified, “chapter-structure-re-implant-with-structure.php” script can be used.

Important modifications in this script before execution:

PHP function “deleteChapterFromStructure()” can be used to delete a chapter. It takes “the chapter id to be deleted” and the “chapter array” as parameters for deletion. This function can be found with commented lines in the script in three positions: main chapter code block, sub chapter code block and sub sub chapter code block.

NOTE: uncomment the lines with this function and modify the parameters in the script in order to delete chapter.

The “chapterStructureControl()” PHP function, controls the positions of the chapter in their respective categories. This function takes “the chapter id in their respective category”, “the position” and the “chapter array” as parameters for execution.

  

  

Scenario 1 (structuring of the main chapter):

- Main chapter id’s are taken from “chapter_main_head” sql table and kept in an array, say here “$chapterArrayWithMainChapterIds”.
    
- Now this array contains say, “1”, “2”, “3”, “4”, “5” values. These values are main chapter ids from the sql table.
    
- Now if we want, id number “5” to be after “1”. Then the value “5” is kept in one PHP variable say, $chapterIdToModify = 5.
    
- The position by printing the “$chapterArrayWithMainChapterIds” array will be “1” as the position for “1” value is “0” and we want the $chapterIdToModify after that. So  $position = 1.
    
- The function will then be chapterStructureControl($chapterIdToModify, $ position, $ chapterArrayWithMainChapterIds). This function returns the modified array which is then further in the script. If no “id” is found for modification, then this function returns an empty array.
    

  

  

Scenario 2 (structuring of the sub chapter):

Same as the scenerion 1 but in order to execute it, first an if-else checking is required with the parent chapter id.

NOTE: Chapters manipulated using this script does not delete or modify the data in the SQL tables associated with the chapter structure. This script only modifies the structure which is used by the program.

Important: Please go through the PHP script carefully, the lines commented can be uncommented to make the functions work in each category i.e main chapter code block,  sub chapter code block and sub sub chapter code block.

Structuring process of chapters is only for developers so, backend sql table analysis of the  chapter id before each execution is necessary. Also, the finally implemented results can be printed for verification of the structure before implantation in the actual chapter control PHP scripts.