---
title : "Bộ nhớ"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Bộ nhớ
Hãy tưởng tượng có các khối bộ nhớ được minh hoạ như hình, áp dụng hệ thống đánh số thập lục phân cho mỗi khối:

![memory blocks](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/2.memory/memory1.png)

Tuy nhiên sẽ dễ gây nhầm lẫn khi khối `10` ở trên đại diện cho một vị trí trong bộ nhớ hoặc giá trị `10`.

Theo quy ước, tất cả các số thập lục phân thường được biểu diễn với tiền tố `0x` như sau:

![memory address](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/2.memory/memory2.png)

Trong cửa sổ terminal, gõ `code addresses.c` và viết mã như sau:
```c
#include <stdio.h>

int main(void)
{
    int n = 50;
}
```

Chúng ta gán số nguyên `50` cho biến `n`. Từ đó, `n` được lưu trữ trong bộ nhớ với giá trị `50`.

Ngôn ngữ C có hai toán tử thường dùng liên quan đến bộ nhớ:

`&` cung cấp địa chỉ của một thông tin được lưu trữ trong bộ nhớ.
`*` chỉ định cho trình biên dịch đến một vị trí trong bộ nhớ.

Áp dụng các toán tử trên vào đoạn mã mới như sau:

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    printf("%p\n", &n);
}
```

`%p` giúp chúng ta xem địa chỉ của một vị trí trong bộ nhớ. `&n` là “địa chỉ của `n`. Thực thi mã này sẽ trả về một địa chỉ trong bộ nhớ bắt đầu bằng 0x.

#### Pointers - Con trỏ
Một ***con trỏ*** là một biến chứa địa chỉ của một giá trị nào đó. Một cách ngắn gọn, con trỏ là một địa chỉ trong bộ nhớ của máy tính.

Ví dụ một đoạn mã dùng con trỏ :

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    int *p = &n;
    printf("%i\n", *p);
}
```
`printf` in ra số nguyên tại vị trí của `p`. `int *p` tạo ra một con trỏ có nhiệm vụ lưu trữ địa chỉ bộ nhớ của số nguyên.