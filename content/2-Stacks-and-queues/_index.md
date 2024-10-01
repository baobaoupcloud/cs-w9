---
title : "Stacks and Queues"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Queues
***Queues*** are one form of abstract data structure.

Queues have specific properties. Namely, they are *FIFO* or “first in first out.” Imagine in a line waiting to buy ice-cream, the first person in the line gets the ice-cream first. The last person is the last to get ice-cream.

Queues have specific actions associated with them. For example, an item can be *enqueued.* It means, the item can join the line or queue. Further, an item can be *dequeued* or leave the queue once it reaches the front of the line.

#### Stacks
***Stacks*** are contrast to queues. Specifically, stacks have the properties of *LIFO* or “last in first out.” Just like stacking trays in a cafeteria, a tray that is placed in a stack last is the first that may be picked up.

Stacks have specific actions associated with them. For example, *push* places something on top of a stack. *Pop* is removing something from the top of the stack.

In code, we might imagine a stack structure defined as follows:

```c
typedef struct{
    person people[CAPACITY];
    int size;
}
stack;
```

Notice that an array called people is of type `person`. The `CAPACITY` is how high the stack could be. The integer `size` is how full the stack actually is, regardless of how much it could hold.

We might imagine that the above code has a limitation. Since the capacity of the array is always predetermined in this code. Therefore, the stack may always be oversized. We might imagine only using one place in the stack out of 5000.

It would be nice for our stack to be dynamic – able to grow as items are added to it.