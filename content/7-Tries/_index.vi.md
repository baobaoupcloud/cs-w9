---
title : "Cây tiền tố"
date :  "`r Sys.Date()`" 
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---
***Trie*** (cây tiền tố) là một dạng cấu trúc dữ liệu khác được sử dụng để lưu trữ một tập hợp chuỗi động. Trie luôn có thể tìm kiếm trong khoảng thời gian xác định. Nó đặc biệt hiệu quả cho các tác vụ như tìm kiếm tiền tố và tự động hoàn thành.

Một nhược điểm của Trie là chúng thường chiếm nhiều bộ nhớ.

Ví dụ từ `Toad` sẽ được lưu trữ như sau:

![tries](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/7.tries/tries1.png)


`Toad` được đánh vần từng chữ cái một, trong đó mỗi chữ cái được liên kết với một danh sách: `T` từ một danh sách, `O` từ một danh sách khác, và cứ như vậy.

Lưu ý rằng chúng ta cần tới 26 x 4 = 104 node chỉ để lưu trữ `Toad`.


Và đó là kết thúc của tuần 5 ^^



