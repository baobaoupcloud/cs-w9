---
title : "Hàm cơ bản"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
### Copy - Sao chép
Một nhu cầu phổ biến trong lập trình là sao chép một chuỗi sang chuỗi khác. Trong cửa sổ terminal, gõ `code copy.c `và viết mã như sau:

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    // Nhận một chuỗi
    string s = get_string("s: ");

    // Sao chép địa chỉ của chuỗi
    string t = s;

    // Viết hoa ký tự đầu tiên trong chuỗi
    t[0] = toupper(t[0]);

    // In chuỗi hai lần
    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```

`string t = s` sao chép địa chỉ của `s` sang `t`. Tuy nhiên lúc này chuỗi không được sao chép – chỉ có địa chỉ là được sao chép.

Để tạo một bản sao thực sự của chuỗi, chúng ta cần hiểu thêm hai thành phần mới. Đầu tiên, `malloc` cho phép chúng ta cấp phát một khối bộ nhớ có kích thước cụ thể. Thứ hai, `free` cho phép chúng ta yêu cầu trình biên dịch giải phóng khối bộ nhớ mà chúng ta đã cấp phát trước đó.

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    // Nhận một chuỗi
    char *s = get_string("s: ");

    // Cấp phát bộ nhớ cho một chuỗi khác
    char *t = malloc(strlen(s) + 1);

    // Sao chép chuỗi vào bộ nhớ, bao gồm '\0'
    for (int i = 0; i <= strlen(s); i++)
    {
        t[i] = s[i];
    }

    // Viết hoa bản sao
    t[0] = toupper(t[0]);

    // In các chuỗi
    printf("s: %s\n", s);
    printf("t: %s\n", t);
    
    // Giải phóng bộ nhớ
    free(t);
    return 0;
}
```
`malloc(strlen(s) + 1)` tạo ra một khối bộ nhớ có độ dài của chuỗi `s` cộng thêm một, bao gồm ký tự null `\0` trong chuỗi đã sao chép. Sau đó, vòng lặp `for` đi qua chuỗi s và gán mỗi giá trị vào vị trí tương ứng trong chuỗi `t`.

#### Swap - Hoán đổi
Một nhu cầu phổ biến khác trong lập trình là hoán đổi hai giá trị. Trong cử sổ terminal, gõ `code swap.c` và viết mã như sau:

```c
#include <stdio.h>

void swap(int *a, int *b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x là %i, y là %i\n", x, y);
    swap(&x, &y);
    printf("x là %i, y là %i\n", x, y);
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```
Lưu ý rằng các biến không được truyền theo giá trị mà theo tham chiếu. Điều đó có nghĩa là địa chỉ của `a` và `b` được cung cấp cho hàm. Do đó, hàm `swap` có thể biết nơi để thực hiện thay đổi đối với `a` và `b` thực tế từ hàm chính.

#### Scan - Quét
Trong CS50, có các hàm như `get_int` để đơn giản hóa việc nhận đầu vào từ người dùng.

`scanf` là một hàm tích hợp có thể nhận đầu vào từ người dùng.

Chúng ta có thể tái triển khai `get_int` bằng cách sử dụng `scanf` như sau:

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
Giá trị của `x` được lưu trữ tại vị trí của `x` trong dòng lệnh `scanf("%i", &x)`.