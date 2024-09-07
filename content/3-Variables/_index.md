---
title : "Variables"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
In C, variables must have a defined data type, and formats code are needed to print them.


**Types:**
- `bool`, a Boolean expression of either true or false
- `char`, a single character like a or 2
- `float`, a floating-point value, or real number with a decimal value
- `double`, a floating-point value with more digits than a float
- `int`, integers up to a certain size, or number of bits
- `long`, integers with more bits, so they can count higher than an int
- `string`, a string of characters


**Format code:**
- `%c`, char
- `%f`, float
- `%i`, int
- `%li`, long int
- `%s`, strings

For example: program to get the user’s name

```bash
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string answer = get_string("What's your name? ");
    printf("hello, %s\n", answer);
}
```
- The `get_string` function is used to get a string from the user. Then, the variable ***answer*** is passed to the ***printf*** function. `%s` is a format code tells the ***printf*** function to prepare itself to receive a string.
- ***answer*** is called a variable. It is of type string and can hold any sting within it.
