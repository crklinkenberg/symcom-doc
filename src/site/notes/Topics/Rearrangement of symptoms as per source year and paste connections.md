---
{"dg-publish":true,"permalink":"/topics/rearrangement-of-symptoms-as-per-source-year-and-paste-connections/"}
---


Whenever comparative symptoms are pasted or paste-edited, the symptoms then appear under its parent in further comparisons.

Source name after comparisons can be like : “1790, Gred 1790_HnRA11 1811_HnRA13 1817_HnRA12 1816_AltHB 1889” and symptoms appear in the order as per their source year.

Example here:

Initial source is: 1790, Gred 1790_HnRA11 1811_ HnRA13 1817

Comparing spurce is: HnRA12 1816_AltHB 1889

Whenever the comparison is displayed fresh, the program will sort and display the initial symptoms in the below pattern:

1. All initials of 1790 with any previous connections (connect, connect edit or swap) of 1811 and 1817. If previous paste connections exist, it will appear below the initials of 1790s.
    
2. All initials of 1811 with any previous connections(connect, connect edit or swap) of 1817.
    
3. All initials of 1817.
    

Technical Details:

Rearrangement of symptoms is done when comparison source is saved, The php function “rearrangeSymptomsInOrder()” is used.

Parameters send to the function:

- `$db`: database connection.
    
- `$comparisonTable`: comparison table name.
    
- `$savedConnectionsComparativeIdsArray`: array containing data of current paste and paste edit symptoms
    
- `$dataPastedId`: array containing data of paste and paste edit ids.
    

 Quelles ids of the comparing is extracted from the table name.

Initials are first inserted in `$savedSortedIdsArray` php array. Then, paste and paste-edit symptoms are inserted after their parents.

According to extracted quelles ids of the comparing, the year of the comparing sources are taken and stored in order.

Comapring are then inserted into `$savedSortedIdsArray` php array as per their year.

The `$savedSortedIdsArray` php array is then returned by the function and this array is used for insertion into the completed table.

The `$savedSortedIdsArray` php array contains symptom ids of the symptom in order as per their source year and pasted connections.