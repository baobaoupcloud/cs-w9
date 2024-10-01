---
title : "Cây"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
***Tree - Cây tìm kiếm nhị phân*** là một cấu trúc dữ liệu khác có thể được sử dụng để lưu trữ dữ liệu một cách hiệu quả hơn, giúp dễ dàng tìm kiếm và truy xuất.

Chúng ta có thể tưởng tượng một chuỗi số đã được sắp xếp.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees1.png)


Hãy tưởng tượng rằng giá trị ở giữa trở thành đỉnh của cây. Những giá trị nhỏ hơn sẽ được đặt ở bên trái, còn những giá trị lớn hơn sẽ ở bên phải.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees2.png)


Các con trỏ có thể được sử dụng để chỉ đến đúng vị trí của từng khu vực bộ nhớ, để mỗi node này có thể được kết nối với nhau.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees3.png)


Trong mã, cấu trúc này có thể được triển khai như sau:

```c
// Tạo danh sách các số dưới dạng cây tìm kiếm nhị phân

#include <stdio.h>
#include <stdlib.h>

// Đại diện cho một node
typedef struct node
{
    int number;             // Giá trị số
    struct node *left;     // Con trỏ đến node bên trái
    struct node *right;    // Con trỏ đến node bên phải
}
node;

void free_tree(node *root);  // Hàm giải phóng bộ nhớ cho cây
void print_tree(node *root); // Hàm in ra cây

int main(void)
{
    // Cây có kích thước 0
    node *tree = NULL;

    // Thêm số vào danh sách
    node *n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1; // Nếu không đủ bộ nhớ, trả về 1
    }
    n->number = 2; // Gán giá trị cho node
    n->left = NULL; // Khởi tạo con trỏ bên trái là NULL
    n->right = NULL; // Khởi tạo con trỏ bên phải là NULL
    tree = n; // Cập nhật cây

    // Thêm số vào danh sách
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free_tree(tree); // Giải phóng bộ nhớ nếu không đủ
        return 1;
    }
    n->number = 1; // Gán giá trị cho node
    n->left = NULL; // Khởi tạo con trỏ bên trái là NULL
    n->right = NULL; // Khởi tạo con trỏ bên phải là NULL
    tree->left = n; // Đặt node này làm node bên trái của cây

    // Thêm số vào danh sách
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free_tree(tree); // Giải phóng bộ nhớ nếu không đủ
        return 1;
    }
    n->number = 3; // Gán giá trị cho node
    n->left = NULL; // Khởi tạo con trỏ bên trái là NULL
    n->right = NULL; // Khởi tạo con trỏ bên phải là NULL
    tree->right = n; // Đặt node này làm node bên phải của cây

    // In cây
    print_tree(tree);

    // Giải phóng cây
    free_tree(tree);
    return 0;
}

void free_tree(node *root)
{
    if (root == NULL)
    {
        return; // Nếu node là NULL, không làm gì cả
    }
    free_tree(root->left);  // Giải phóng cây bên trái
    free_tree(root->right); // Giải phóng cây bên phải
    free(root); // Giải phóng node hiện tại
}

void print_tree(node *root)
{
    if (root == NULL)
    {
        return; // Nếu node là NULL, không làm gì cả
    }
    print_tree(root->left); // In cây bên trái
    printf("%i\n", root->number); // In ra giá trị số tại node hiện tại
    print_tree(root->right); // In cây bên phải
}
```
Giải thích: hàm tìm kiếm bắt đầu bằng cách đi đến vị trí của `tree`. Sau đó, nó sử dụng đệ quy để tìm kiếm `number`. Hàm `free_tree` sẽ giải phóng cây theo cách đệ quy. Hàm `print_tree` cũng thực hiện việc in cây theo cách đệ quy.

Một cây như trên mang lại tính linh hoạt mà một mảng không có. Nó có thể tăng lên và thu nhỏ theo nhu cầu của chúng ta. Hơn nữa, cấu trúc này còn có thể được tìm kiếm nhanh.



