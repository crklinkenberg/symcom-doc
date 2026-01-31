Dated: 28th August, 2024
The user view page link of the development section had been used by Carl in last few weeks by mistake and since changes are already done to that particular source. This user view listing was supposed to be used by him for presentation and the viewer might view the user view page around December. 

Since, it is in development environment we can't risk it as modification to user view section may arise at any time. Hence, a copy of databases have been done and the user view page data which was in the development have now been isolated and is preserved.

Any modification or changes of data in the development or stage environment will not affect the preserved user view data. It is hosted inside stage environment or PHP functions inside stage might impact the preserved user view UI.

Database changes:
```
User view database: alegra_new_repertory_user_final_view_important
Main database: development_repertory_for_user_view
```

File changes:
```
New directory user-view is created with files inside dev-exp directory.
```

Link: [http://www.stage.reference-repertory.com/dev-exp/user-view-demo/](http://www.stage.reference-repertory.com/dev-exp/user-view-demo/)

