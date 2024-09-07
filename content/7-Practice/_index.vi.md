---
title : "Thực hành"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
Everything discussed above can be applied to create code representing the blocks in **Mario**. For example: 

Build the horizontal blocks of 4 `?`
![mario](/images/7.practice/1practice.png)
In the terminal window, type `code mario.c` and code as follows:

```bash
#include <stdio.h>

int main(void)
{
for (int i = 0; i < 4; i++)
    {
        printf("?");
    }
    printf("\n");
}
```
Similarly, we can create vertical blocks of 3
![mario](/images/7.practice/2practice.png)

Modify the code as follows:
```bash
#include <stdio.h>

int main(void)
{
for (int i = 0; i < 3; i++)
    {
        printf("#\n");
    }
}
```
Show the results by executing `make mario` in the terminal window, followed by `./mario`.


And that's all for week 1 ^^