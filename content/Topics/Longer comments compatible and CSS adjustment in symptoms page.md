---
{"dg-publish":true,"permalink":"/topics/longer-comments-compatible-and-css-adjustment-in-symptoms-page/"}
---


Improvements:
Added CSS class `comment_css` for `$row['Kommentar']` in `symptoms.php` script.
assets/css/custom.css
Inside script:
```
/* larger comment css */
.comment_css{
  max-height: 150px; /* You can change this to your preferred height */
  overflow-y: auto;  /* Enables vertical scrollbar when content overflows */
  padding: 10px;
}
```

SQL changes with query done for development, staging and production databases:
```sql
ALTER TABLE `quelle_import_master` CHANGE `import_comment` `import_comment` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'Comment (@C)';

ALTER TABLE `temp_quelle_import_master` CHANGE `import_comment` `import_comment` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'Comment (@C)';

ALTER TABLE `quelle_import_master_backup` CHANGE `import_comment` `import_comment` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT 'Comment (@C)';
```
