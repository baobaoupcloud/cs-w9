---
title : "Loops"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
#### Heap and Stack
***Heap*** and ***stack*** refer to two different types of memory used for managing data during program execution. 

***Stack*** is a region of memory. When a function is called, a block of memory (called a stack frame) is allocated on the stack for local variables, function parameters, and return addresses.

Memory on the stack is automatically managed. It gets allocated when a function is called and deallocated when it returns.

A ***stack overflow*** is when too many functions are called, overflowing the amount of memory available. It can cause a program to crash or behave unpredictably. The operating system typically detects this and may terminate the program.

***Heap*** is a pool of memory used for dynamic memory allocation. Unlike the stack, the heap does not have a strict LIFO order. Memory on the heap must be manually managed. It remains allocated until it is explicitly deallocated using `free()`.

A ***heap overflow*** occurs when a program writes more data to a block of memory on the heap than it was allocated for. This can lead to data corruption or security vulnerabilities.

#### Valgrind
***Valgrind*** is a tool that can check to see if there are memory-related issues with our programs wherein we utilized `malloc`. Specifically, it checks to see if we `free` all the memory allocated.

Consider the following code for `memory.c`:

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *x = malloc(3 * sizeof(int));
    x[1] = 72;
    x[2] = 73;
    x[3] = 33;
}
```

Notice that running this program does not cause any errors. While `malloc` is used to allocate enough memory for an array, the code fails to `free` that allocated memory.

If we type `make memory` followed by `valgrind ./memory`, we will get a report from valgrind that will report where memory has been lost as a result of our program. 

One error valgrind reveals is that we attempted to assign the value of `33` at the 4th position of the array, where we only allocated an array of size `3`. Another error is that we never freed `x`.

We can modify our code as follows:

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *x = malloc(3 * sizeof(int));
    x[0] = 72;
    x[1] = 73;
    x[2] = 33;
    free(x);
}
```

Then running valgrind again now results in no memory leaks.

#### Garbage values

When we ask the compiler for a block of memory, there is no guarantee that this memory will be empty.

It’s very possible that this memory that we allocated was previously utilized by the computer. Accordingly, we may see *junk* or *garbage values*. This is a result of getting a block of memory but not initializing it. For example, consider the following code for `garbage.c`:

```c
#include <stdio.h>

int main(void)
{
    int scores[1024];
    for (int i = 0; i < 1024; i++)
    {
        printf("%i\n", scores[i]);
    }
}
```

Running this code will allocate `1024` locations in memory for our array, but the `for` loop will likely show that not all values therein are `0`. It’s always best practice to be aware of the potential for garbage values when we do not initialize blocks of memory to some other value like zero or otherwise.

And that's all of week 4 ^^