---
title : "Chuỗi"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
#### Chuỗi
Một chuỗi đơn giản là một mảng các ký tự. Ví dụ, `string s = "HI!"` có thể được biểu diễn như sau:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/3.strings/strings1.png)

`s` cần được lưu trữ ở đâu đó. Chúng ta có thể hình dung mối quan hệ của `s` với chuỗi như sau:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/3.strings/strings2.png)

Con trỏ `s` cho trình biên dịch biết vị trí byte đầu tiên của chuỗi trong bộ nhớ.

Xem đoạn mã sau:

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
Đoạn mã trên in ra các vị trí trong bộ nhớ của từng ký tự trong chuỗi `s`. Ký hiệu `&` dùng để hiển thị địa chỉ của từng phần tử trong chuỗi. Khi chạy mã này, hãy lưu ý rằng các phần tử `0`, `1`, `2` và `3` nằm liền kề nhau trong bộ nhớ.

Tương tự, chúng ta có thể sửa lại mã như sau:

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%s\n", s);
}
```

Mã này sẽ hiển thị chuỗi bắt đầu từ vị trí của `s`. Mã này chính là mã thô để lấy chuỗi mà không sử dụng thư viện `cs50.h`.

#### Toán tử con trỏ
Chúng ta có thể sử dụng các toán tử khác để hiển thị chuỗi như sau:

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%c\n", s[0]);
    printf("%c\n", s[1]);
    printf("%c\n", s[2]);
}
```
Chúng ta đang in ra từng ký tự tại vị trí của `s`.

Ngoài ra có thể thay thế bằng đoạn mã này:

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

Ký tự đầu tiên tại vị trí của `s` được in ra. Sau đó lại in ra ký tự tại vị trí `s + 1`, và cứ thế tiếp tục.



