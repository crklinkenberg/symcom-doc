---
{"dg-publish":true,"permalink":"/topics/rules-applicable-to-new-refactored-database-tables/"}
---


1. All entity tables are in plural form. 
	For example: user tables is named as users. Medicines, Testers etc.
2. If table name consists of multiple words to define their meaning, the words are separated with `"_"`.
		For example: Table `english_synonyms`.
3. Relationship tables with composite keys are given prefix "`rel_"` with the associated table names in singular form.
	For example: Relationship between roles and users tables is stored in SQL table named `"rel_role_user"`.
4. Temporary tables are given prefix `"temp_"`.
5. Temporary tables used during the import process are given prefix `"itemp_"`.
6. Dynamic tables such as tables formed during comparison process are named differently.
	Comparison table: `comparison_table_arzneiID_initialSourceID_comparingSourceID_comparisonLanguage` 
	Connection table: Comparison table name followed by suffix `"_connections"`
	Highest matches table: Comparison table name followed by suffix `"_highest_matches"`
	Completed table: Comparison table name followed by suffix `"_completed"`
	History table: Comparison table name with prefix `"history_"`.
7. ID field in table name follows convention "singular form of table name" followed by suffix `'_id'`.
	For example in users table, user id is named as `'user_id'`.
8. ID field of dynamic SQL tables are named only "id".
9. Primary key attributes are "UNSIGNED".
10. Five audit columns: `ip_address, editor_id, creator_id, created_at, updated_at` are added to each SQL tables.
11. All table names and fields are in English language.
12. History tables for a comparison is created dynamically when a comparison is finalized and saved by the supervisor.
13. Tables in the database should follow 3NF level of normalization.
14. For chaptering process, a different database with name `"symptom_classification"` is used by the python program. The chapter ID defined in that database are globally accepted by the `Symcom` program. Any change in chapter name or structure in that database will be effective in throughout the program.
15. It is advised to always escape symptom strings which may contain special characters before insertion to SQL tables.