---
title : "Điều kiện"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
Câu lệnh điều kiện là các cấu trúc thực hiện các hành động khác nhau tùy thuộc vào điều kiện đưa ra.


Ví dụ, chúng ta có thể dùng câu lệnh điều kiện để viết chương trình so sánh hai số:
1. Trong cửa sổ terminal, gõ `code compare.c` và viết mã như sau:
```bash
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int x = get_int("Nhập số x: ");
    int y = get_int("Nhập số y: ");

if (x < y)
    {
        printf("x nhỏ hơn y\n");
    }
elseif (x > y)
    {
        printf("x lớn hơn y\n");
    }
else{
        printf("x bằng y\n");
    }
}
```
Chúng ta đã tạo 2 biến kiểu số nguyên x và y. Giá trị của 2 biến này được nhập bằng hàm `get_int`. Quy trình bắt đầu kiểm tra điều kiện của `if`. Nếu điều kiện được thỏa mãn, hàm sẽ trả về giá trị tương ứng. Nếu điều kiện không được đáp ứng, logic sẽ tiếp tục kiểm tra điều kiện tiếp theo `elseif`. Cuối cùng, nếu không có điều kiện nào được thỏa mãn, logic sẽ trả về giá trị của `else`.

2. Để chạy mã, gõ `make compare` trong cửa sổ terminal, sau đó gõ `./compare`.
3. Nhập 2 số nguyên và xem kết quả.

Quá trình chạy của chương trình có thể được thể hiện dưới dạng **lưu đồ thuật toán**. Chúng ta có thể kiểm tra hiệu quả của đoạn mã dựa trên các biểu đồ này.

Dưới đây là lưu đồ thuật toán của mã trên.
![flowchart](https://github.com/baobaoupcloud/cs/blob/main/static/images/4.conditionals/2conditionals.png?raw=true)
