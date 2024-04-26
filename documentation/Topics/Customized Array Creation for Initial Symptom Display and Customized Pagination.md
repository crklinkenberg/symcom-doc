This array `$customizedInitialArray[]` is sent to “initialCustomListingModified()” PHP function for final display of initial symptoms in the comparison page. This array is a return from different functions which are responsible for customized filtration of symptoms in the comparison page.

On the basis of `$unmarkedInitialsCheck` value, different cases runs which gives this array final values. `$unmarkedInitialsCheck` value:

1 => for unmarked initials display.

2 => for general non secure initial display.

3 => for non secure connect connection display.

4 => for non secure paste connection display.

5 => for display of all connections except normal connect and normal swap.

	For unmarked, general non secure, non secure connect and non secure paste, “pastetNsArray(), connectNsArray(), generalNsArray(), markingInitialArray()” functions are used. These functions searches the initial via SQL query and returns the initial ids to this customized array.
		
	For display of all connections except normal connect and normal swap: In this case customNsListings() functions is used. Basic workflow:

  

- SQL query is executed in the connections table. Initial ids, connection type, non secure connect and earlier connection flag for each search results are put in separate arrays.
    
- Case for multiple connect connection under same initial with no non secure connections are taken and then excluded from the final initial arrays.
    
- Case for only single connection under one initial which is connect and not non secure connect is taken and then excluded from the final initial arrays.
    
- Similar cases for swap normal connect cases are also taken and excluded.
    
- In brief: For each initial ids’, their key values are taken from the array, each key value is synchronized with non-secure connect, connection type and earlier connection arrays and overall process is executed using PHP predefined functions.
    
- Final array is returned from the function and is then used for comparison process.
    
- The total number of elements of this customized array and per page initial symptoms are finally used for display of initials in the comparison page.