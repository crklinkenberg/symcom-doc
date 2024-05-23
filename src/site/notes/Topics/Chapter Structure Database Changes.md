---
{"dg-publish":true,"permalink":"/topics/chapter-structure-database-changes/"}
---


Below SQL queries are executed after the classification database is created in the server.
```SQL
-- Changes in chapter_main_head sql table.
-- Column is added
ALTER TABLE chapter_main_head
ADD COLUMN structure_id INT DEFAULT 0;

-- All values are set as per id
SET @counter = 0;

UPDATE chapter_main_head
SET structure_id = (@counter := @counter + 1)
ORDER BY id;


-- Changes in chapter_sub_head sql table
-- Column is added
ALTER TABLE chapter_sub_head
ADD COLUMN structure_id INT DEFAULT 0;

-- All values are set as per id
SET @counter = 0;

UPDATE chapter_sub_head
SET structure_id = (@counter := @counter + 1)
ORDER BY id;


-- Changes in chapter_sub_head sql table
-- Column is added
ALTER TABLE chapter_sub_sub_head
ADD COLUMN structure_id INT DEFAULT 0;

-- All values are set as per id
SET @counter = 0;

UPDATE chapter_sub_sub_head
SET structure_id = (@counter := @counter + 1)
ORDER BY id;

-- structure_id changed to varchar
ALTER TABLE `chapter_main_head` CHANGE `structure_id` `structure_id` VARCHAR(11) NULL DEFAULT '0';

ALTER TABLE `chapter_sub_head` CHANGE `structure_id` `structure_id` VARCHAR(11) NULL DEFAULT '0';

ALTER TABLE `chapter_sub_sub_head` CHANGE `structure_id` `structure_id` VARCHAR(11) NULL DEFAULT '0';

--adding chapter weight
ALTER TABLE `symptom_chapter_assignment` ADD `chapter_weight` INT(10) NOT NULL DEFAULT '0' AFTER `chapter_id`;
```

