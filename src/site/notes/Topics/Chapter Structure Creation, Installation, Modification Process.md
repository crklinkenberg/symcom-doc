---
{"dg-publish":true,"permalink":"/topics/chapter-structure-creation-installation-modification-process/"}
---

#### Chapter Structure Installation:

Chapter Structure can be initially installed following the chapter classification python program.
When the python classification program is installed, the chapter structure and its related database tables are installed in the server.

#### Chapter Structure Modification:
In the chapter structure tables: `chapter_main_head`, `chapter_sub_head`, `chapter_sub_sub_head`, a column `structure_id` exists which controls the structure of the chapters.

The value of this id can be decimal and if new chapter is to be added under any main chapter or sub chapters, the values can be manipulated so that the new chapter appears in order as desired. 

Here's an illustration:

Suppose the below is data from  `chapter_main_head` SQL table.

| id  | main_head_en | main_head_de | structure_id |
| --- | ------------ | ------------ | ------------ |
| 1   | Vertigo      | Schwindel    | 1            |
| 2   | Head, outer  | Kopf, außen  | 2            |

and suppose the below is data from  `chapter_sub_head` SQL table.

| id  | sub_head_en        | sub_head_de              | parent_main_head_id | structure_id |
| --- | ------------------ | ------------------------ | ------------------- | ------------ |
| 1   | General outer head | Allgemeiner äußerer Kopf | 2                   | 1            |
| 2   | Temples            | Tempel                   | 2                   | 2            |

We can see that the Head, outer main chapter has two sub chapters with id 1 and 2 respectively.
If a new chapter is to be added in before sub chapter with id 2 that is Temples, then the new added chapter row should contain `structure_id` value less than the `structure_id` value of Temples chapter. In this case, we can take values like `1.9`. So the `chapter_sub_head` tables will now changes like this:

| id  | sub_head_en        | sub_head_de              | parent_main_head_id | structure_id |
| --- | ------------------ | ------------------------ | ------------------- | ------------ |
| 1   | General outer head | Allgemeiner äußerer Kopf | 2                   | 1            |
| 2   | Temples            | Tempel                   | 2                   | 2            |
| 3   | Skull              | Schädel                  | 2                   | 1.9          |

This will ensure the chapter sub chapter Skull always comes before Temples when chapter structure is displayed and used in the program.

In this case, the chapter structure during display will be :
```
Vertigo
Head, outer
	General outer head
	Skull
	Temples
```

#### Important PHP functions related to chapters:

`getAllChapters()`: This function retrieves the chapter structure from the database based on the `structure_id`.

`getAllChaptersWithPagination(start_page, per_page_chapters, master_chapter_arr))`: This function helps retrieve chapters in parts. This is useful assigned symptoms are listed under chapter structure and the accommodating large chapter structure with symptoms becomes difficult in a single web page.


