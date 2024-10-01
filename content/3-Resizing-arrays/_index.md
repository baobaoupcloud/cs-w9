---
title : "Resizing Arrays"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
Imagine we have an array of 3 numbers `1, 2, 3`. In memory, there are other values being stored by other programs, functions, and variables. Many of these may be unused garbage values that were utilized at one point but are available now for use.

![123 array](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays1.png)

Imagine we wanted to store a fourth value `4`in our array? What would be needed is to allocate a new area of memory and move the old array to a new one. Initially, this new area of memory would be populated with garbage values.

![resizing](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays2.png)

As values are added to this new area of memory, old garbage values would be overwritten.

![resize](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays3.png)

One of the drawbacks of this approach is that it’s bad design: Every time we add a number, we have to copy the array item by item.

Building upon our knowledge obtained in previous weeks, we can leverage our understanding of pointers to create a better design.

In the terminal, type `code list.c` and write code as follows:

```c
// Implements a list of numbers with an array of dynamic size

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // List of size 3
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }

    // Initialize list of size 3 with numbers
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;

    // List of size 4
    int *tmp = malloc(4 * sizeof(int));
    if (tmp == NULL)
    {
        free(list);
        return 1;
    }

    // Copy list of size 3 into list of size 4
    for (int i = 0; i < 3; i++)
    {
        tmp[i] = list[i];
    }

    // Add number to list of size 4
    tmp[3] = 4;

    // Free list of size 3
    free(list);

    // Remember list of size 4
    list = tmp;

    // Print list
    for (int i = 0; i < 4; i++)
    {
        printf("%i\n", list[i]);
    }

    // Free list
    free(list);
    return 0;
}
```

Notice that a list of size three integers is created. Then, three memory addresses are assigned the values `1`, `2`, and `3`. Then, a list of size four is created. Next, the list is copied from the first to the second. The value for the `4` is added to the `tmp` list. Since the block of memory that `list` points to is no longer used, it is freed using the command `free(list)`. Finally, the compiler is told to point `list` pointer now to the block of memory that `tmp` points to. The contents of `list` are printed and then freed.