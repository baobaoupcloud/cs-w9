---
title : "Variables"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
#### Strings

Recall that a string is simply an array of characters. For example, `string s = "HI!"` can be represented as follows:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/3.strings/strings1.png)

As you can imagine, `s` needs to be stored somewhere. We can visualize the relationship of `s` to the string as follows:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/3.strings/strings2.png)

The pointer called `s` tells the compiler where the first byte of the string exists in memory.

Consider the following code:

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string s = "HI!";
    printf("%p\n", s);
    printf("%p\n", &s[0]);
    printf("%p\n", &s[1]);
    printf("%p\n", &s[2]);
    printf("%p\n", &s[3]);
}
```

The above prints the memory locations of each character in the string `s`. The `&` symbol is used to show the address of each element of the string. When running this code, notice that elements `0`, `1`, `2`, and `3` are next to one another in memory.

Likewise, we can modify our code as follows:

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%s\n", s);
}
```

This code will present the string that starts at the location of `s`. This code effectively removes the training wheels of the `string` data type offered by `cs50.h`. Above is raw C code to get string without using the cs50 library. 

#### Pointer arithmetic

We can modify the code to accomplish the same thing in a longer form as follows:

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%c\n", s[0]);
    printf("%c\n", s[1]);
    printf("%c\n", s[2]);

```

We are printing each character at the location of `s`.

Further, we can modify the code as follows:

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%c\n", *s);
    printf("%c\n", *(s + 1));
    printf("%c\n", *(s + 2));
}
```

Notice that the first character at the location of `s` is printed. Then, the character at the location `s + 1` is printed, and so on.