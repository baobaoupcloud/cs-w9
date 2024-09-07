---
title : "Lập trình bằng ngôn ngữ C"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
Trong khoá học này, chúng ta sử dụng **Visual Studio Code** (VS Code) làm môi trường phát triển tích hợp (IDE). VS Code đã được cài đặt sẵn tất cả các phần mềm cần thiết cho khóa học.


Chúng ta sử dụng ba lệnh để viết, biên dịch và chạy chương trình: `code`, `make`, `./` 

Ví dụ: xây dựng chương trình hello
1. Mở cửa sổ terminal, gõ ```code hello.c``` để tạo một tệp C có tên là hello và cho phép chúng ta viết các hướng dẫn cho chương trình này.

2. Trong trình soạn thảo vừa xuất hiện, viết mã như sau:
 ```bash
#include <stdio.h>

int main(void)
{
    printf("chào bạn\n");
}
```
`printf` là hàm để xuất dòng văn bản. Chú ý vị trí dấu ngoặc đơn `()` và dấu chấm phẩy `;`. Kế đó, `\n` để thêm một dòng mới sau từ "chào bạn". Các hàm khác sẽ được đề cập sau trong khóa học.

3. Trong cửa sổ terminal, gõ ```make hello``` hoặc ```clang hello.c -o hello``` để biên dịch tệp từ chỉ thị của chúng ta và tạo ra một tệp thực thi tên là hello.
4. Tiếp tục gõ ```./hello``` để chạy chương trình hello.
5. Chương trình sẽ thực thi và hiển thị "chào bạn".

Trong ngôn ngữ lập trình C, chúng ta có các thư viện hàm. Có một [trang tài liệu hướng dẫn](https://manual.cs50.io/) tổng hợp các hàm và thư viện tương ứng. Các hàm này đã được viết sẵn từ trước và có thể sử dụng lại trong mã của mình.

{{% notice Lưu ý %}}
Ở đầu mã, nhớ thêm tệp tiêu đề để sử dụng các hàm. Ví dụ thêm tệp tiêu đề stdio.h `#include <stdio.h>` để dùng hàm `printf`. Lưu ý 2: các câu lệnh mã phải kết thúc bằng dấu `;` . Quên `;` sẽ gây ra lỗi.
{{% /notice %}}

