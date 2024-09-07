---
title : "Loops"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
A **loop** is a sequence of instructions that is continually repeated until a certain condition is reached. 

For example we can loop the action saying meow 3 times in 2 ways: ***while loop*** and ***for loop***.

1. Initially, the code looks like this:
```bash
#include <stdio.h>

int main(void)
{
    printf("meow\n");
    printf("meow\n");
    printf("meow\n");
}
```
2. We can improve the code by using ***while loop***:
```bash
#include <stdio.h>

int main(void)
{
    int i = 0;
    while (i < 3)
    {
        printf("meow\n");
        i++;
    }
}
```
The code means `i` variable type integer is assigned the value `0`. We create a **while loop** that will run as long as `i < 3`. Then, the loop runs. Every time `1` is added to `i` using the `i++` statement.

3. Or we can use the ***for loop***:
```bash
#include<stdio.h>

int main(void)
{
for (int i = 0; i < 3; i++)
    {
        printf("meow\n");
    }
}
```
The first argument `int i = 0` starts our counter at `0`. The second argument `i < 3` is the condition that is being checked. Finally, the argument `i++` tells the loop to add `1` each time the loop runs.

{{% notice note %}} 
***For loop*** is used when the number of iterations is known, whereas execution is done in a ***while loop*** until the statement in the program is proved wrong, we do not know how many loops there would be.
{{% /notice %}} 
