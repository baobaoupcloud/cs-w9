---
title : "Pixel"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
#### Pixel
***Pixels*** là những ô vuông, các điểm riêng lẻ, có màu sắc được sắp xếp trên một lưới theo chiều dọc và chiều ngang.

Chúng ta có thể tưởng tượng như một bản đồ của các bit, trong đó số không đại diện cho màu đen và số một đại diện cho màu trắng.

![pixel art](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/1.pixel/pixel1.png)

*RGB* (red, green, blue: đỏ, xanh lá, xanh dương), là các giá trị đại diện cho lượng các màu trên. Trong Adobe Photoshop, chúng ta có thể thấy các thiết lập như hình dưới:

![color picker](https://raw.githubusercontent.com/baobaoupcloud/cs-w4/main/static/images/1.pixel/pixel2.png)

Lượng màu đỏ, xanh dương và xanh lá làm thay đổi màu sắc được chọn.

Chúng ta có thể thấy rằng màu sắc không chỉ được đại diện bởi ba giá trị. Ở dưới cùng của cửa sổ, có một giá trị đặc biệt được tạo thành từ các số và ký tự. `255` được đại diện là `FF`, một giá trị hệ thập lục phân.

#### Hệ thập lục phân
***Hệ thập lục phân*** là một hệ thống đếm có 16 giá trị gồm:

`0 1 2 3 4 5 6 7 8 9 a b c d e f`

`a` đại diện cho `10` và cứ thế, `f` đại diện cho `15`.

Hệ thập lục phân còn được gọi là cơ số 16.

Khi đếm trong hệ thập lục phân, mỗi cột là một lũy thừa của 16.

- Số `0` được đại diện là `00`.
- Số `1` được đại diện là `01`.
- Số `10` được đại diện là `0A`.
- Số `11` được đại diện là `0B`.
- Số `15` được đại diện là `0F`.
- Số `16` được đại diện là `10`.
- Số `255` được đại diện là `FF`, vì 16 x 15 (`F`) là 240. Thêm 15 nữa để đạt 255. Đây là số lớn nhất mà chúng ta có thể đếm được bằng hệ thập lục phân hai chữ số.

Hệ thập lục phân rất hữu ích vì nó dễ sử dụng và giúp biểu diễn thông tin một cách ngắn gọn.