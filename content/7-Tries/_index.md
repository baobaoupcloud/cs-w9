---
title : "Tries"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
***Tries*** are another form of data structure used for storing a dynamic set of strings. Tries are always searchable in constant time. It's particularly efficient for tasks like prefix searching and autocomplete.
One downside to Tries is that they tend to take up a large amount of memory.

`Toad` would be stored as follows:

![tries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/7.tries/tries1.png)

`Toad` being spelled with one letter at a time where one letter is associated with one list T from one list O from another and so on.

Notice that we need 26 x 4 = 104 nodes just to store `Toad`


And that’s the end of week 5 ^^