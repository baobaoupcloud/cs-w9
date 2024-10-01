---
title : "Dictionaries"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
#### Dictionaries
***Dictionaries*** are another data structure. Dictionaries essentially, like actual book-form dictionaries that have a word and a definition, have a *key* and a *value*. 

Keys can often be of various types (strings, numbers, etc.), and values can be of any data type. Each key is unique and is used to retrieve the associated value efficiently.

Dictionaries can offer such speed of access through hashing.

#### Hashing
***Hashing*** is the idea of taking a value and being able to output a value that becomes a shortcut to it later.

For example, hashing `*apple*` may hash as a value of `1`, and `*berry*` may be hashed as `2`. Therefore, finding `*apple*` is as easy as asking the `*hash*` algorithm where `1` is stored. A hashed value can be used to shortcut finding such a value.

A *hash function* is an algorithm that reduces a larger value to something small and predictable. Generally, this function takes in an item we wish to add to the hash table, and returns an integer representing the array index in which the item should be placed.

A *hash table* is a combination of both arrays and linked lists. When implemented in code, a hash table is an *array* of *pointers* to *node*s.

A hash table could be imagined as follows:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash1.png)

Notice that this is an array that is assigned each value of the alphabet.

Then, at each location of the array, a linked list is used to track each value being stored there:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash2.png)

*Collisions* are when we add values to the hash table, and something already exists at the hashed location. In the above, collisions are simply appended to the end of the list.

Collisions can be reduced by better programming the hash table and hash algorithm. Imagine an improvement upon the above as follows:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash3.png)

We have to make a decision about the advantages of using more memory to have a large hash table and potentially reducing search time or using less memory and potentially increasing search time.