---
title : "AJAX và API"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
**Asynchronous JavaScript and XML** (AJAX) là sự kết hợp của các công nghệ phát triển ứng dụng web, giúp ứng dụng web tương tác nhanh hơn với người dùng. Mỗi khi người dùng tương tác với ứng dụng web, chẳng hạn như khi họ nhấp vào các nút hoặc chọn hộp kiểm, trình duyệt sẽ trao đổi dữ liệu với máy chủ từ xa.

**Application Programming Interface (API)** là tập hợp các quy tắc cho phép bạn tương tác với một dịch vụ khác. Ví dụ, chúng ta có thể sử dụng **API của IMDB** để truy cập vào cơ sở dữ liệu của họ. Chúng ta thậm chí có thể tích hợp các API để xử lý các loại dữ liệu cụ thể có thể tải xuống từ server.

Ví dụ code của `app.py` như sau:

```python
# Tìm kiếm chương trình bằng cách sử dụng Ajax

from cs50 import SQL
from flask import Flask, render_template, request

app = Flask(__name__)

db = SQL("sqlite:///shows.db")

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/search")
def search():
    q = request.args.get("q")
    if q:
        shows = db.execute("SELECT * FROM shows WHERE title LIKE ? LIMIT 50", "%" + q + "%")
    else:
        shows = []
    return render_template("search.html", shows=shows)
```

Route tìm kiếm thực hiện một lệnh SQL để tìm kiếm chương trình.

Nội dung trong `search.html` rất đơn giản:

```html
{% for show in shows %}
    <li>{{ show["title"] }}</li>
{% endfor %}
```

Tệp cung cấp danh sách gạch đầu dòng.

Cuối cùng, trong `index.html`, ta thấy mã **AJAX** được sử dụng để hỗ trợ việc tìm kiếm:

```html
<!DOCTYPE html>

<html lang="vi">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>Chương trình</title>
    </head>
    <body>

        <input autocomplete="off" autofocus placeholder="Tìm kiếm" type="search">

        <ul></ul>

        <script>
            let input = document.querySelector('input');
            input.addEventListener('input', async function() {
                let response = await fetch('/search?q=' + input.value);
                let shows = await response.text();
                document.querySelector('ul').innerHTML = shows;
            });
        </script>

    </body>
</html>
```

Một **event listener** được sử dụng để truy vấn server nhằm cung cấp danh sách các chương trình phù hợp với tiêu đề mà người dùng nhập vào. Điều này sẽ tìm đến thẻ `ul` trong HTML và thay đổi nội dung của trang web để hiển thị danh sách kết quả phù hợp.
