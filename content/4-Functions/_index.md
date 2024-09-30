---
title : "Conditionals"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
#### Copy

A common need in programming is to copy one string to another. In the terminal window, type `code copy.c` and write code as follows:

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    // Get a string
    string s = get_string("s: ");

    // Copy string's address
    string t = s;

    // Capitalize first letter in string
    t[0] = toupper(t[0]);

    // Print string twice
    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```

`string t = s` copies the address of `s` to `t`. This does not accomplish what we are desiring. The string is not copied – only the address is.

To make an authentic copy of the string, we will need to introduce two new building blocks. First, `malloc` allows us to allocate a block of a specific size of memory. Second, `free` allows us to tell the compiler to *free up* that block of memory we previously allocated.

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    // Get a string
    char *s = get_string("s: ");

    // Allocate memory for another string
    char *t = malloc(strlen(s) + 1);

    // Copy string into memory, including '\0'
    for (int i = 0; i <= strlen(s); i++)
    {
        t[i] = s[i];
    }

    // Capitalize copy
    t[0] = toupper(t[0]);

    // Print strings
    printf("s: %s\n", s);
    printf("t: %s\n", t);
    
    // Free memory
    free(t);
    return 0;
}
```

`malloc(strlen(s) + 1)` creates a block of memory that is the length of the string `s` plus one. This allows for the inclusion of the *null* `\0` character in our final copied string. Then, the `for` loop walks through the string `s` and assigns each value to that same location on the string `t`.

#### Swap

In the real world, a common need in programming is to swap two values. In practice, we can type `code swap.c` and write code as follows:

```c
include <stdio.h>

void swap(int *a, int *b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(&x, &y);
    printf("x is %i, y is %i\n", x, y);
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

Notice that variables are not passed by *value* but by *reference*. That is, the addresses of `a` and `b` are provided to the function. Therefore, the `swap` function can know where to make changes to the actual `a` and `b` from the main function.

#### Scanf

In CS50, there are functions like `get_int` to simplify the act of getting input from the user.

`scanf` is a built-in function that can get user input.

We can reimplement `get_int` rather easily using `scanf` as follows:

```c
#include <stdio.h>

int main(void)
{
    int x;
    printf("x: ");
    scanf("%i", &x);
    printf("x: %i\n", x);
}
```

The value of `x` is stored at the location of `x` in the line `scanf("%i", &x)`.