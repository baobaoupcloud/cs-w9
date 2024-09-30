---
title : "Heap và Stack"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
#### Heap và Stack
***Heap*** và ***stack*** đề cập đến hai loại bộ nhớ khác nhau được sử dụng để quản lý dữ liệu trong quá trình thực thi chương trình.

***Stack*** là bộ nhớ cấp phát tĩnh. Khi một hàm được gọi, một khối bộ nhớ (gọi là stack frame) được cấp phát trên stack cho các biến cục bộ, tham số hàm và địa chỉ trả về.

Bộ nhớ trên stack được quản lý tự động. Nó được cấp phát khi một hàm được gọi và được giải phóng khi hàm đó trả về.

***Stack overflow*** xảy ra khi quá nhiều hàm được gọi, làm tràn lượng bộ nhớ có sẵn. Điều này có thể khiến chương trình gặp sự cố hoặc hoạt động không ổn định. Hệ điều hành thường phát hiện điều này và có thể chấm dứt chương trình.

***Heap*** là bộ nhớ cấp phát động. Khác với stack, bộ nhớ trên heap phải được quản lý thủ công. Nó sẽ vẫn được cấp phát cho đến khi được giải phóng rõ ràng bằng cách sử dụng `free()`.

***Heap overflow*** xảy ra khi một chương trình ghi nhiều dữ liệu hơn vùng đã được cấp phát. Điều này có thể dẫn đến hỏng dữ liệu hoặc lỗ hổng bảo mật.

#### Valgrind
***Valgrind*** là một công cụ giúp kiểm tra vấn đề liên quan đến bộ nhớ trong các chương trình mà đã sử dụng `malloc`. Cụ thể, nó sẽ kiểm tra xem chúng ta đã giải phóng tất cả bộ nhớ đã được cấp phát hay chưa.

Hãy xem đoạn mã sau, gỡ `code memory.c`:

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *x = malloc(3 * sizeof(int));
    x[1] = 72;
    x[2] = 73;
    x[3] = 33;
}
```
Khi chạy chương trình này sẽ không gây ra lỗi. Nhưng nếu chúng ta chạy `make memory` và `valgrind ./memory`, chúng ta sẽ nhận được một thông báo từ valgrind cho biết nơi nào bộ nhớ đã bị mất.

Valgrind phát hiện lỗi rằng chúng đã cố gắng gán giá trị `33` vào vị trí thứ 4 của mảng, trong khi chúng ta chỉ cấp phát một mảng có kích thước là 3. Một lỗi khác là chúng ta chưa giải phóng `x`.

Chúng ta có thể sửa đổi mã như sau:

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *x = malloc(3 * sizeof(int));
    x[0] = 72;
    x[1] = 73;
    x[2] = 33;
    free(x);
}
```
Sau đó, chạy lại valgrind sẽ không còn phát sinh rò rỉ bộ nhớ nữa.

#### Giá trị rác
Khi chúng ta yêu cầu trình biên dịch cấp phát một khối bộ nhớ,sẽ không chắc chắn rằng bộ nhớ này sẽ trống.

Rất có thể bộ nhớ mà chúng ta cấp phát đã được máy tính sử dụng trước đó. Do đó, chúng ta có thể thấy các giá trị rác. Điều này xảy ra do việc cấp phát một khối bộ nhớ nhưng không khởi tạo nó. Ví dụ đoạn mã, `code garbage.c`:

```c
#include <stdio.h>

int main(void)
{
    int scores[1024];
    for (int i = 0; i < 1024; i++)
    {
        printf("%i\n", scores[i]);
    }
}
```
Chạy mã này sẽ cấp phát 1024 vị trí trong bộ nhớ cho mảng, với vòng lặp `for` có thể cho thấy rằng không phải tất cả các giá trị trong đó đều là `0`. Tạo thói quen nhớ rằng có thể xuất hiện các giá trị rác nếu chúng ta không khởi tạo các khối bộ nhớ với một giá trị cụ thể, chẳng hạn như số không hoặc giá trị khác.

Và đó là kết thúc cho tuần 4 ^^