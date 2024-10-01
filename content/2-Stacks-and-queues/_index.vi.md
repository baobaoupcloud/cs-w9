---
title : "Hàng đợi và Ngăn xếp"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Queues - Hàng đợi
***Queues*** là một dạng cấu trúc dữ liệu trừu tượng.

Queues có những đặc tính cụ thể. Đó là FIFO hay "first in first out" (đến trước, phục vụ trước). Hãy tưởng tượng bạn đang xếp hàng để mua kem, người đứng đầu hàng sẽ nhận kem trước. Người đứng cuối hàng sẽ là người nhận kem cuối cùng.

Queues có những tác vụ cụ thể liên quan. Ví dụ, một mục có thể được **enqueued**, có nghĩa là mục đó có thể gia nhập vào hàng đợi. Ngoài ra, một mục có thể được **dequeued** hoặc rời khỏi hàng đợi khi nó đến lượt ở đầu hàng.

#### Stacks - Ngăn xếp
***Stacks*** có những đặc tính ngược lại với queues. Cụ thể, stacks có tính chất LIFO hay "last in first out" (đến sau, phục vụ trước). Giống như việc xếp đĩa trong một căng tin, đĩa được đặt vào ngăn xếp cuối cùng sẽ là đĩa đầu tiên được lấy ra.

Stacks cũng có những tác vụ cụ thể liên quan. Ví dụ, **push** là đặt một mục lên trên cùng của ngăn xếp. **Pop** là loại bỏ một mục từ phía trên cùng ngăn xếp.

Có thể tưởng tượng một cấu trúc stack được định nghĩa như sau:

```c
typedef struct{
    person people[CAPACITY];
    int size;
}
stack;
```

Giải thích: định nghĩa một mảng `people` có kiểu `person`. `CAPACITY` là dung lượng tối đa của stack. Số nguyên `size` là mức độ đầy của stack, bất kể nó có thể chứa bao nhiêu.

Chúng ta có thể hiểu rằng mã trên có một số giới hạn. Bởi vì dung lượng của mảng luôn được xác định trước trong mã này nên stack có thể luôn bị thừa. Chúng ta có thể chỉ sử dụng một chỗ trong stack trong tổng số 5000.

Sẽ tốt hơn nếu stack động – có khả năng mở rộng khi có các mục được thêm vào.