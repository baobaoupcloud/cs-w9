---
title : "Operators and functions"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
**Operators** are the mathematical operations that are supported by the compiler. In C, these mathematical operators include:
- `+` for addition
- `-` for subtraction
- `*` for multiplication
- `/` for division
- `%` for remainder

For example: assign the sum of a and b to c:  `int c = a + b;`


We can create our own **functions** in C. For example create a C function called meow  
```bash
    void meow(void)
    {
        printf("meow\n");
    }
``` 
With `meow` is the name of the function we want to create. The first `void` means this function has no return value. And the `void` in parentheses means it takes no inputs. It only meows