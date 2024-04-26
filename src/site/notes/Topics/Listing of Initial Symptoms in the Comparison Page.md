---
{"dg-publish":true,"permalink":"/topics/listing-of-initial-symptoms-in-the-comparison-page/"}
---


Listing of initial symptoms are dynamic. Not only the normal display but customized display of non secure connections and unmarked initials are all done in the “comparison.php” page using the `initialCustomListingModified($param, $db, $comparison_table, $page_start, $per_page_initial, $customized_array)` PHP function.

This function takes database connection, comparison table name, start value of page, per page initial symptom number, value for handling the function and a customized array as parameters.

$param values:

1 => for unmarked initials display.

2 => for general non secure initial display.

3 => for non secure connect connection display.

4 => for non secure paste connection display.

5 => for display of all connections except normal connect and normal swap.

other(default) => normal display of initials with connections and comparing symptoms.

`$customized_array`: PHP array sent from pagination function to control the number of initials to be displayed. This array is  different and has different values.

This array is associated with “customNsListings(), pastetNsArray(), connectNsArray(), generalNsArray(), markingInitialArray()” PHP functions which are all responsible for display of initials and the pagination control of the comparison page.

  

Basic Workflow of initialCustomListingModified() function:

  

- The total count for the customized array is taken out. It is then used for customized pagination.
    
- According to start value of the page and the per page initial symptom number, a new PHP array `$displayInitialArray[]` is created using the `$customized_array[]` values.
    
- For each id’s of the `$displayInitialArray[]` array, modified SQL query (as per the value for handling the function) is executed and the info of the initial id is taken out and stored in `$allInitialInfo[]` array. This array is then returned by the function and is used for display in the comparison page.