---
title : "Linked Lists"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
A ***linked list*** is one of the most powerful data structures within C. A linked list allows us to include values that are located at varying areas of memory. Further, they allow us to dynamically grow and shrink the list as we desire.

We will use following primitives:

- `struct` is a data type that we can define ourselves.
- `.` allows us to access variables inside that structure.
- `*` operator is used to declare a pointer or dereference a variable.
- `->` operator goes to an address and looks inside of a structure.

Imagine three values stored at three different areas of memory as follows:

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists1.png)

To stitch together these values in a list, we could utilize more memory to keep track of where the next item is.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlist2.png)

`NULL` is used to indicate that nothing else is next in the list. 

By convention, we would keep one more element in memory, a pointer, that keeps track of the first item in the list.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists3.png)

Abstracting away the memory addresses, the list would appear as follows:

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists4.png)

These boxes are called ***nodes***. A *node* contains both an `*item*` and a pointer called `*next*`. In code, we can imagine a node as follows:

```c
typedef struct node
{
    int number;
    struct node *next;
}
node;
```

The item contained within this node is an integer called `number`. Second, a pointer to a node called `next` is included, which will point to another node somewhere in memory.

Conceptually, we can imagine the process of creating a linked list. First, `node *list` is declared, but it is of a garbage value.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists5.png)

Next, a node called `n` is allocated in memory.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists6.png)

Next, the `number` of node `n` is assigned the value `1`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists7.png)

Next, the node’s `next` field is assigned `NULL`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists8.png)

Next, `list` is pointed at the memory location to where `n` points. `n` and `list` now point to the same place.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists9.png)

A new node is then created. Both the `number` and `next` field are both filled with garbage values.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists10.png)

The `number` value of `n`’s node (the new node) is updated to `2`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists11.png)

Also, the `next` field is updated as well.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists12.png)

Most important, we do not want to lose our connection to any of these nodes lest they be lost forever. Accordingly, `n`’s `next` field is pointed to the same memory location as `list`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists13.png)

Finally, `list` is updated to point at `n`. We now have a linked list of two items.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists14.png)

To implement this in code, write `code list.c` as follows:

```c
// Implements a list of numbers using a linked list

#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
}
node;

int main(int argc, char *argv[])
{
    // Memory for numbers
    node *list = NULL;

    // For each command-line argument
    for (int i = 1; i < argc; i++)
    {
        // Convert argument to int
        int number = atoi(argv[i]);

        // Allocate node for number
        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            return 1;
        }
        n->number = number;
        n->next = NULL;

        // If list is empty
        if (list == NULL)
        {
            // This node is the whole list
            list = n;
        }

        // If list has numbers already
        else
        {
            // Iterate over nodes in list
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // If at end of list
                if (ptr->next == NULL)
                {
                    // Append node
                    ptr->next = n;
                    break;
                }
            }
        }
    }

    // Print numbers
    for (node *ptr = list; ptr != NULL; ptr = ptr->next)
    {
        printf("%i\n", ptr->number);
    }

    // Free memory
    node *ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next;
        free(ptr);
        ptr = next;
    }
}
```

Notice that what the user inputs at the command line is put into the `number` field of a node called `n`, and then that node is added to the `list`. For example, `./list 1 2` will put the number `1` into the `number` field of a node called `n`, then put a pointer to `list` into the `next` field of the node, and then update `list` to point to `n`. That same process is repeated for `2`. Next, `node *ptr = list` creates a temporary variable that points at the same spot that `list` points to. The `while` prints what at the node `ptr` points to, and then updates `ptr` to point to the `next` node in the list. Finally, all the memory is freed.

Linked lists are not stored in a contiguous block of memory. They can grow as large as you wish, provided that enough system resources exist. The downside, however, is that more memory is required to keep track of the list instead of an array. This is because for each element, we must store not just the value of the element, but also a pointer to the next node. 

Further, linked lists cannot be indexed into like is possible in an array because we need to pass through the first `n−1` elements to find the location of the `n`  element. Because of this, the list pictured above must be linearly searched, binary search is not possible.

We can create a list that is sorted when items are added:
```c
// Implements a sorted list of numbers using a linked list

#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
}
node;

int main(int argc, char *argv[])
{
    // Memory for numbers
    node *list = NULL;

    // For each command-line argument
    for (int i = 1; i < argc; i++)
    {
        // Convert argument to int
        int number = atoi(argv[i]);

        // Allocate node for number
        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            return 1;
        }
        n->number = number;
        n->next = NULL;

        // If list is empty
        if (list == NULL)
        {
            list = n;
        }

        // If number belongs at beginning of list
        else if (n->number < list->number)
        {
            n->next = list;
            list = n; 
        }

        // If number belongs later in list
        else
        {
            // Iterate over nodes in list
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // If at end of list
                if (ptr->next == NULL)
                {
                    // Append node
                    ptr->next = n;
                    break;
                }

                // If in middle of list
                if (n->number < ptr->next->number)
                {
                    n->next = ptr->next;
                    ptr->next = n;
                    break;
                }
            }
        }
    }

    // Print numbers
    for (node *ptr = list; ptr != NULL; ptr = ptr->next)
    {
        printf("%i\n", ptr->number);
    }

    // Free memory
    node *ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next;
        free(ptr);
        ptr = next;
    }
}
```