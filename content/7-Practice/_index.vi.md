---
title : "Thực hành"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
Chúng ta có thể áp dụng các phần học trong tuần này để tạo khối trong **Mario**. Ví dụ: 

Dựng thanh ngang tạo bởi 4 khối `?`
![mario](https://raw.githubusercontent.com/baobaoupcloud/cs/main/static/images/7.practice/1practice.png)
Trong cửa sổ terminal, gõ `code mario.c` và viết mã như sau:

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
Tương tự, chúng ta có thể tạo cột dọc từ 3 khối
![mario](https://raw.githubusercontent.com/baobaoupcloud/cs/main/static/images/7.practice/2practice.png)

Viết đoạn mã như sau:
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
Gõ `make mario` trong cửa sổ terminal và `./mario` để xem thành quả.



Và, hết 1 tuần học ^^
