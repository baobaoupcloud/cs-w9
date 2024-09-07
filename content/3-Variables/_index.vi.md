---
title : "Biến"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
Trong ngôn ngữ lập trình C, các biến phải có kiểu dữ liệu và các mã định dạng cần thiết để in ra.


**Các kiểu dữ liệu:**
- `bool`, biểu thức boolean với giá trị đúng (true) hoặc sai (false)
- `char`, ký tự như a hoặc 2
- `float`, số thực với giá trị thập phân
- `double`, số thực với nhiều chữ số hơn float
- `int`, số nguyên với kích thước nhất định, hoặc số bit
- `long`, số nguyên với nhiều bit hơn, nên có thể đếm nhiều hơn kiểu int
- `string`, chuỗi các ký tự


**Mã định dạng:**
- `%c`, (char) ký tự
- `%f`, (float) số thực
- `%i`, (int) số nguyên
- `%li`, (long int) số nguyên lớn hơn
- `%s`, (strings) chuỗi ký tự

Ví dụ: tạo chương trình lấy tên của người dùng

```bash
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string answer = get_string("Bạn tên là? ");
    printf("chào, %s\n", answer);
}
```
- Hàm `get_string` dùng để lấy chuỗi ký tự từ người dùng. Sau đó, biến ***answer*** được truyền vào hàm ***printf***. Mã định dạng `%s` giúp hàm ***printf*** chuẩn bị xác định sẽ nhận mội chuỗi ký tự.
- ***answer*** được gọi là một biến có kiểu dữ liệu 'string' (chuỗi ký tự) có thể chứa bất kỳ chuỗi nào.
