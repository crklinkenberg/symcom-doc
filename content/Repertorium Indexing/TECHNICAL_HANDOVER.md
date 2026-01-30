---
dg-publish: true
---

# Repertorium - Technical Handover Documentation

## Overview
Repertorium is a medical data management system built with **CodeIgniter 3**, **Smarty Templating**, and **Grocery CRUD**.

## Core Architecture
- **Framework**: CodeIgniter 3.x.
- **Database**: MySQL/MariaDB.
- **CRUD Operations**: Driven by [Grocery CRUD](https://www.grocerycrud.com/documentation), which handles most table operations (list, add, edit, delete).
- **Templates**: Smarty (.tpl files located in `application/views`).
- **Base Controllers**:
    - `MY_SmartyController`: Integrates Smarty.
    - `MY_SmartyCRUDController`: Integrates Grocery CRUD.
    - `MY_DefaultController`: Adds standard fields like `ErstellerID`, `ErstellerDatum`, `Stand`.

## Key Component: Indexierung (Indexing)
The Indexing functionality is the most complex part of the system.
- **Controller**: `application/controllers/optionen/Indexierung.php`
- **Logic**: It generates dynamic forms based on the `fundstelle` table.
- **Configuration Tables**:
    - `kategorie`: Parent ID 7 defines the different "Forms" (e.g., Symptomlisten, Kasuistik).
    - `fundstellefeld`: Defines all possible fields for indexing.
    - `fundstelleformfeld`: Links specific fields to specific forms and marks them as `Required` or not.
- **Validation**: Custom validation callbacks (e.g., `_check_SeitePDFBis`) are implemented in the `Indexierung` controller.

## Known Issues and Recent Fixes (January 2026)
1. **Indexing Permissions**: Historically, some groups (like 'symcom') lacked access to Indexing menu items. This is handled via the `permissions` table and the `view_navigation` SQL view.
2. **Variable Typos**: A bug in `Fundstelleform_model.php` (line 65) where `$row` was used instead of `$result` was fixed.
3. **Validation Typos**: `Indexierung.php` had a typo in `_check_SeitePDFBis` which was previously fixed.
4. **Author Creation**: Identified that the `autor` table has strict `NOT NULL` constraints (e.g., for `Code`) which were missing from the UI forms, causing save failures.
5. **N:N Validation**: Many-to-many relationships (like Authors for an Index entry) may fail "Required" validation if the field name is not correctly suffixed with `[]` in the validation rules.

## Database Schema Highlights
- `navigation`: Stores the menu structure.
- `permissions`: Links groups/users to navigation IDs.
- `autor`: Stores authors/editors.
- `fundstelle`: The main table for storing indexed data.
- `kategorie`: Universal category table (used for forms, countries, types, etc.).

## Development Checklist for New Programmers
- Use `MY_Grocery_CRUD` for all standard table management.
- When adding fields to a table, check if they need to be added to the corresponding controller's `fields()` list.
- If a field is `NOT NULL` in the DB, ensure it is either in the form or populated via `callback_before_insert`.
- For many-to-many relationships, use `$crud->set_relation_n_n()`.
