---
title : "Memory"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Memory
Imagine there are blocks of memory visualised as follows, applying hexadecimal numbering to each:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/2.memory/memory1.png)

But it might seem confusing when the block `10` above represent a location in memory or the value `10`. 

Accordingly, by convention, all hexadecimal numbers are often represented with the `0x` prefix as follows:

![memory address](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/2.memory/memory2.png)

In the terminal window, type `code addresses.c` and write the code as follows:

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
}
```

We assign the integer `50` to variable `n` . So `n` is stored in memory with the value `50`.

The `C` language has two powerful operators that relate to memory:

- `&` provides the address of something stored in memory.
- `*` instructs the compiler to go to a location in memory.

We can leverage this knowledge by modifying our code as follows:

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n);
}
```

Notice the `%p`, which allows us to view the address of a location in memory. `&n` can be literally translated as “the address of `n`.” Executing this code will return an address of memory beginning with `0x`.

#### Pointers

A pointer is a variable that contains the address of some value. Most succinctly, a pointer is an address in our computer’s memory.

To illustrate the use of the `*` operator, consider the following:

```c
#include *<stdio.h>*

int main(void)
{
    int n = 50;
    int *p = &n;
    printf("%i**\n**", *p);
}
```

Notice that the `printf` line prints the integer at the location of `p`. `int *p` creates a pointer whose job is to store the memory address of an integer.