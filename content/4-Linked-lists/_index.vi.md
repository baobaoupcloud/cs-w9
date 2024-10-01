---
title : "Danh sách liên kết"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
***Linked list*** (danh sách liên kết) là một trong những cấu trúc dữ liệu mạnh mẽ nhất trong C. Nó cho phép chúng ta lưu trữ các giá trị nằm ở những vùng bộ nhớ khác nhau. Hơn nữa, linked list cho phép chúng ta mở rộng hoặc thu nhỏ danh sách một cách linh hoạt theo từng nhu cầu.

Chúng ta sẽ sử dụng các phần tử cơ bản sau:

- `struct` là kiểu dữ liệu mà chúng ta có thể tự định nghĩa.
- `.` cho phép truy cập các biến bên trong cấu trúc đó.
- `*` được sử dụng để khai báo một con trỏ hoặc giải tham chiếu một biến.
- `->` giúp truy cập vào một địa chỉ và đi vào bên trong một cấu trúc.


Hãy tưởng tượng ba giá trị được lưu trữ tại ba vùng bộ nhớ khác nhau như sau:

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists1.png)


Để kết nối các giá trị này thành một danh sách, chúng ta có thể sử dụng thêm bộ nhớ để theo dõi vị trí của mục tiếp theo.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlist2.png)


`NULL` được sử dụng để chỉ ra rằng không còn gì khác trong danh sách.

Theo quy ước, chúng ta sẽ giữ một phần tử bổ sung trong bộ nhớ, đó là một con trỏ, dùng để theo dõi mục đầu tiên trong danh sách.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists3.png)


Bỏ qua các địa chỉ bộ nhớ, danh sách sẽ xuất hiện như sau:

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists4.png)


Các ô này được gọi là nodes. Một node chứa một *item* và một con trỏ gọi là *next*. Trong mã, chúng ta có thể tưởng tượng một node như sau:

```c
typedef struct node
{
    int number;
    struct node *next;
}
node;
```

Phần tử chứa trong node này là một số nguyên có tên là `number`. Thứ hai, nó bao gồm một con trỏ tới một node khác gọi là `next`, sẽ trỏ tới một node nào đó trong bộ nhớ.

Về mặt khái niệm, chúng ta có thể hình dung quá trình tạo một linked list như sau. Đầu tiên, `node *list` được khai báo, nhưng nó sẽ có giá trị rác.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists5.png)


Tiếp theo, một node gọi là `n` được cấp phát trong bộ nhớ.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists6.png)


Sau đó, giá trị `number` của node `n` được gán là `1`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists7.png)


Tiếp theo, trường `next` của node được gán là `NULL`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists8.png)


Sau đó, `list` được trỏ tới địa chỉ mà `n` đang trỏ tới. Bây giờ, `n` và `list` đều trỏ tới cùng một vị trí.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists9.png)


Một node mới sau đó được tạo ra. Cả trường `number` và `next` đều được lấp đầy bằng các giá trị rác.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists10.png)


Giá trị `number` của node `n` (node mới) được cập nhật thành `2`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists11.png)


Trường `next` lúc này cũng được cập nhật.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists12.png)


Quan trọng nhất, chúng ta không muốn mất kết nối với bất kỳ node nào trong số này để không bị lạc mất. Do đó, trường `next` của `n` được trỏ tới cùng một địa chỉ bộ nhớ như `list`.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists13.png)


Cuối cùng, `list` được cập nhật để trỏ tới `n`. Chúng ta đã có một linked list gồm hai mục.

![lists](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/4.linkedlists/linkedlists14.png)


Để triển khai điều này trong mã, hãy viết `code list.c` như sau:

```c
// Tạo một danh sách các số sử dụng linked list

#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
}
node;

int main(int argc, char *argv[])
{
    // Bộ nhớ cho các số
    node *list = NULL;

    // Đối với mỗi tham số dòng lệnh
    for (int i = 1; i < argc; i++)
    {
        // Chuyển đổi tham số thành int
        int number = atoi(argv[i]);

        // Cấp phát node cho số
        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            return 1;
        }
        n->number = number;
        n->next = NULL;

        // Nếu danh sách rỗng
        if (list == NULL)
        {
            // Node này là toàn bộ danh sách
            list = n;
        }

        // Nếu danh sách đã có số
        else
        {
            // Lặp qua các node trong danh sách
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // Nếu ở cuối danh sách
                if (ptr->next == NULL)
                {
                    // Thêm node
                    ptr->next = n;
                    break;
                }
            }
        }
    }

    // In các số
    for (node *ptr = list; ptr != NULL; ptr = ptr->next)
    {
        printf("%i\n", ptr->number);
    }

    // Giải phóng bộ nhớ
    node *ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next;
        free(ptr);
        ptr = next;
    }
}
```
Chú ý rằng những gì người dùng nhập vào dòng lệnh sẽ được đưa vào trường `number` của node gọi là `n`, và sau đó node đó sẽ được thêm vào `list`. Ví dụ, gõ lệnh `./list 1 2` sẽ đưa số `1` vào trường `number` của node gọi là `n`, sau đó sẽ đặt một con trỏ tới `list` vào trường `next` của node, và cập nhật `list` để trỏ tới `n`. Quá trình này sẽ được lặp lại cho số `2`. Tiếp theo, `node *ptr = list` tạo ra một biến tạm thời trỏ tới cùng một vị trí mà `list` trỏ tới. Vòng lặp `while` sẽ in ra nội dung của node mà `ptr` trỏ tới và sau đó cập nhật `ptr` để trỏ tới node tiếp theo trong danh sách. Cuối cùng, tất cả bộ nhớ sẽ được giải phóng.

Linked lists không được lưu trữ trong một khối bộ nhớ liên tiếp. Chúng có thể mở rộng lớn hơn tùy ý, miễn là có đủ tài nguyên hệ thống. Tuy nhiên, nhược điểm là cần nhiều bộ nhớ hơn để theo dõi danh sách thay vì một mảng. Chúng ta không chỉ phải lưu giá trị của phần tử mà còn phải lưu một con trỏ tới node tiếp theo.

Hơn nữa, linked lists không thể được truy cập theo chỉ số như trong một mảng vì chúng ta cần phải đi qua n−1 phần tử đầu tiên để tìm vị trí của phần tử thứ n. Do đó, danh sách như hình trên phải được tìm kiếm tuần tự, không thể tìm kiếm nhị phân.

Chúng ta có thể tạo một danh sách được sắp xếp trong khi các mục được thêm vào:

```c
// Tạo một danh sách được sắp xếp các số sử dụng linked list

#include <cs50.h>
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;             // Số nguyên
    struct node *next;     // Con trỏ tới node tiếp theo
}
node;

int main(int argc, char *argv[])
{
    // Bộ nhớ cho các số
    node *list = NULL;

    // Đối với mỗi tham số dòng lệnh
    for (int i = 1; i < argc; i++)
    {
        // Chuyển đổi tham số thành int
        int number = atoi(argv[i]);

        // Cấp phát node cho số
        node *n = malloc(sizeof(node));
        if (n == NULL)
        {
            return 1; // Nếu không đủ bộ nhớ, trả về 1
        }
        n->number = number; // Gán giá trị cho trường number
        n->next = NULL;     // Khởi tạo trường next là NULL

        // Nếu danh sách rỗng
        if (list == NULL)
        {
            list = n; // Node này là toàn bộ danh sách
        }

        // Nếu số thuộc về đầu danh sách
        else if (n->number < list->number)
        {
            n->next = list; // Đặt node mới vào đầu danh sách
            list = n;       // Cập nhật list trỏ tới node mới
        }

        // Nếu số thuộc về vị trí sau trong danh sách
        else
        {
            // Lặp qua các node trong danh sách
            for (node *ptr = list; ptr != NULL; ptr = ptr->next)
            {
                // Nếu ở cuối danh sách
                if (ptr->next == NULL)
                {
                    ptr->next = n; // Thêm node vào cuối danh sách
                    break;
                }

                // Nếu ở giữa danh sách
                if (n->number < ptr->next->number)
                {
                    n->next = ptr->next; // Đặt con trỏ tới node tiếp theo
                    ptr->next = n;       // Chèn node mới vào giữa
                    break;
                }
            }
        }
    }

    // In các số
    for (node *ptr = list; ptr != NULL; ptr = ptr->next)
    {
        printf("%i\n", ptr->number); // In ra số ở node hiện tại
    }

    // Giải phóng bộ nhớ
    node *ptr = list;
    while (ptr != NULL)
    {
        node *next = ptr->next; // Lưu trữ node tiếp theo
        free(ptr);              // Giải phóng node hiện tại
        ptr = next;            // Cập nhật ptr tới node tiếp theo
    }
}
