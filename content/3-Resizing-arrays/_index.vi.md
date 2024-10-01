---
title : "Thay đổi kích thước mảng"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
Hãy tưởng tượng chúng ta có một mảng gồm 3 số `1, 2, 3`. Trong bộ nhớ, còn có nhiều giá trị khác đang được lưu trữ bởi các chương trình, hàm và biến khác. Nhiều giá trị trong số này có thể là các giá trị rác chưa được sử dụng hay từng được sử dụng ở một thời điểm nào đó nhưng hiện tại có sẵn để sử dụng.

![123 array](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays1.png)


Giả sử chúng ta muốn lưu trữ một giá trị thứ tư là `4` trong mảng. Chúng ta cần phải cấp phát một vùng bộ nhớ mới và di chuyển mảng cũ sang vùng mới này. Ban đầu, vùng bộ nhớ mới sẽ được lấp đầy bằng các giá trị rác.

![resizing](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays2.png)


Khi các giá trị được thêm vào vùng bộ nhớ mới, các giá trị rác cũ sẽ bị ghi đè.

![resize](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/3.resizing-arrays/resizingarrays3.png)


Một trong những nhược điểm của cách tiếp cận này là thiết kế không tối ưu. Mỗi khi chúng ta thêm một số, chúng ta phải sao chép từng phần tử của mảng.

Dựa trên những kiến thức đã học ở các tuần trước, chúng ta có thể tận dụng con trỏ để tối ưu thiết kế.
Trong terminal, gõ `code list.c` và viết mã như sau:
```c
// Tạo một danh sách các số với mảng có kích thước động

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // Danh sách có kích thước 3
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }

    // Gán danh sách với các số
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;

    // Tạo danh sách có kích thước 4
    int *tmp = malloc(4 * sizeof(int));
    if (tmp == NULL)
    {
        free(list);
        return 1;
    }

    // Sao chép danh sách kích thước 3 vào danh sách kích thước 4
    for (int i = 0; i < 3; i++)
    {
        tmp[i] = list[i];
    }

    // Thêm số mới vào danh sách kích thước 4
    tmp[3] = 4;

    // Giải phóng danh sách kích thước 3
    free(list);

    // Nhớ danh sách kích thước 4
    list = tmp;

    // In danh sách
    for (int i = 0; i < 4; i++)
    {
        printf("%i\n", list[i]);
    }

    // Giải phóng danh sách
    free(list);
    return 0;
}
```

Giải thích: một danh sách có kích thước ba số nguyên được tạo ra. Sau đó, ba địa chỉ bộ nhớ được gán các giá trị `1, 2, và 3`. Tiếp theo, một danh sách có kích thước bốn được tạo ra. Danh sách cũ được sao chép sang danh sách mới. Giá trị `4` được thêm vào danh sách `tmp`. Vì khối bộ nhớ mà `list` trỏ tới không còn được sử dụng, nó sẽ được giải phóng bằng lệnh free(list). Cuối cùng, chúng ta cập nhật con trỏ `list` để trỏ tới khối bộ nhớ mà `tmp` đang trỏ tới. Nội dung của `list` được in ra và sau đó cũng được giải phóng.