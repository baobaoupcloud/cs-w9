---
title : "Toán tử và hàm"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
**Toán tử** là các phép toán được trình biên dịch hỗ trợ. Trong C, các toán tử toán học bao gồm:
- `+` để cộng
- `-` để trừ
- `*` để nhân
- `/` để chia
- `%` để lấy dư


Ví dụ: gán tổng của a và b cho c:  `int c = a + b;`


Chúng ta có thể tự tạo **hàm** trong C. Ví dụ, tạo một hàm `meow`:
```bash
    void meow(void)
    {
        printf("meow\n");
    }
``` 
Trong đó, `meow` là tên của hàm mà chúng ta muốn tạo. Từ `void` đầu tiên có nghĩa là hàm này không có giá trị trả về. Từ `void` trong dấu ngoặc đơn có nghĩa là hàm không nhận đầu vào. Hàm này chỉ đơn giản là in ra "meow".
