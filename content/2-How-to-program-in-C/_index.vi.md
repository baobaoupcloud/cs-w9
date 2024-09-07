---
title : "Lập trình bằng ngôn ngữ C"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
In this course, we use **Visual Studio Code** (VS Code) as the integrated development environment (IDE). VS Code has all the software required for the course already pre-loaded on it.

We use three commands to write, compile, and run our program: `code`, `make`, `./` 

For example: build the program hello
1. Go into the terminal window, type ```code hello.c``` to creates a file in C named hello and allows us to type instructions for this program.

2. In the text editor that appears, write code as follows:
 ```bash
#include <stdio.h>

int main(void)
{
    printf("hello, mate\n");
}
```
`printf` is a function that can output a line of text. Notice the placement of the quotes `()` and the semicolon `;`. Further, the `\n` creates a new line after the words "hello, mate". Other functions will be mentioned later in the course.

3. In the terminal window, type ```make hello``` or ```clang hello.c -o hello``` to compile the file from our instruction and creates an executable file called hello
4. Continue type ```./hello``` to run the program hello
5. The program will execute saying "hello, mate"

In C, we have libraries of functions. There is a [Manual](https://manual.cs50.io/) provides all the capabilities of them. They are collections of pre-written functions that others have written in the past that we can utilise in our code.

{{% notice note %}}
At the start of the code, remember to include the header file to use the functions. Such as `#include <stdio.h>` to use `printf` function. Also notice that the statement of code is closed with a `;` . Omission of `;` will cause error.
{{% /notice %}}

