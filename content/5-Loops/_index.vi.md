---
title : "Vòng lặp"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
Một **vòng lặp** là một chuỗi các lệnh được lặp đi lặp lại liên tục cho đến khi đạt đến điều kiện nhất định.

Ví dụ, chúng ta có thể lặp hành động in từ "meow" 3 lần bằng 2 cách: vòng lặp ***while*** và vòng lặp ***for***.

1. Với đoạn mã ban đầu:
```bash
#include <stdio.h>

int main(void)
{
    printf("meow\n");
    printf("meow\n");
    printf("meow\n");
}
```
2. Chúng ta có thể sử dụng ***vòng lặp while*** tối ưu hơn:
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
Đoạn này có nghĩa là, biến số nguyên `i` được gán giá trị = `0`. Chúng ta tạo ***vòng lặp while*** chạy lặp đi lặp lại đến khi `i < 3`. Mỗi lần lặp, biến `i` sẽ được cộng thêm `1` bằng câu lệnh `i++`.

3. Hoặc có thể sử dụng ***vòng lặp for***:
```bash
#include <stdio.h>

int main(void)
{
for (int i = 0; i < 3; i++)
    {
        printf("meow\n");
    }
}
```
Đối số đầu tiên `int i = 0` xem như điểm bắt đầu bộ đếm từ `0`. Đối số tiếp theo là điều kiện để kiểm tra `i < 3`. Và đối số cuối cùng `i++` để thực hiện phép cộng `1` vào biến `i` mỗi lần vòng lặp chạy.


{{% notice note %}}
***Vòng lặp for*** thường dùng khi biết trước số lần lặp, còn ***Vòng lặp while*** được lặp liên tục đến khi đạt điều kiện, chúng ta có thể không biết rõ số lần lặp.
{{% /notice %}}
