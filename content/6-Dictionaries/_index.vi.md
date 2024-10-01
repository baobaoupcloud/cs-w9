---
title : "Từ điển"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---
#### Dictionary - Từ điển
***Từ điển*** là một cấu trúc dữ liệu khác. Giống như từ điển nghĩa đen, có từ và định nghĩa, nó có một khóa và một giá trị.

Khóa thường có thể thuộc nhiều loại khác nhau (chuỗi, số,...), và giá trị có thể là bất kỳ loại dữ liệu nào. Mỗi khóa là duy nhất và được sử dụng để truy xuất giá trị liên quan.

Từ điển có thể cung cấp tốc độ truy cập nhanh nhờ vào **hash** (băm).

#### Hash - Băm
Băm là việc lấy một giá trị và xuất ra một giá trị khác chính là lối tắt cho nó sau này.

Ví dụ, từ `táo` có thể băm thành giá trị `1`, và `chanh` có thể được băm thành `2`. Từ đó, việc tìm `táo` sẽ dễ như việc hỏi thuật toán *hash* nơi mà `1` được lưu trữ. Một giá trị đã được băm có thể được sử dụng như một lối tắt để tìm giá trị đó.

Một hàm băm là một thuật toán biến một giá trị lớn thành một thứ nhỏ hơn và có thể dự đoán được. Thông thường, hàm này sẽ nhận một mục mà chúng ta muốn thêm vào bảng băm và trả về một số nguyên đại diện cho chỉ số mảng nơi mà mục đó nên được đặt.

Một bảng băm là sự kết hợp giữa mảng và danh sách liên kết. Khi được triển khai trong mã, một bảng băm là một mảng của các con trỏ đến các node.

Một bảng băm có thể được tưởng tượng như sau:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash1.png)


Đây là một mảng được gán cho mỗi giá trị của bảng chữ cái.

Sau đó, tại mỗi vị trí của mảng, một danh sách liên kết được sử dụng để theo dõi mỗi giá trị được lưu trữ ở đó:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash2.png)


Mâu thuẫn sẽ xảy ra khi ta thêm giá trị vào bảng băm một cái gì đó đã tồn tại trước vị trí đã băm. Trong trường hợp này, các va chạm sẽ được thêm vào cuối danh sách.

Điều này có thể được giảm thiểu bằng cách lập trình bảng băm và thuật toán băm tối ưu hơn như sau:

![dictionaries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/6.dictionaries/hash3.png)

Chúng ta phải cân nhắc chọn giữa sử dụng nhiều bộ nhớ hơn để có một bảng băm lớn và có khả năng giảm thời gian tìm kiếm, hoặc sử dụng ít bộ nhớ hơn và có khả năng tăng thời gian tìm kiếm.



