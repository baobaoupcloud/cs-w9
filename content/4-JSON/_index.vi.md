---
title : "JSON"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
**JavaScript Object Notation (JSON)** là một định dạng văn bản của các đối tượng từ điển với các khóa và giá trị. Đây là cách đơn giản và thân thiện với máy tính để lấy được nhiều dữ liệu.

JSON được hoạt động như trong đoạn code ở `index.html`:

```html
<!DOCTYPE html>

<html lang="vi">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>Chương trình</title>
    </head>
    <body>

        <input autocomplete="off" autofocus placeholder="Tìm kiếm" type="text">

        <ul></ul>

        <script>
            let input = document.querySelector('input');
            input.addEventListener('input', async function() {
                let response = await fetch('/search?q=' + input.value);
                let shows = await response.json();
                let html = '';
                for (let id in shows) {
                    let title = shows[id].title.replace('<', '&lt;').replace('&', '&amp;');
                    html += '<li>' + title + '</li>';
                }
                document.querySelector('ul').innerHTML = html;
            });
        </script>

    </body>
</html>
```

Ngoài ra, có thể xem cách phản hồi JSON được lấy ra trong  `app.py`:

```python
# Tìm kiếm chương trình bằng Ajax với JSON

from cs50 import SQL
from flask import Flask, jsonify, render_template, request

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
    return jsonify(shows)
```

`jsonify` được sử dụng để chuyển kết quả thành định dạng dễ đọc và có thể chấp nhận được bởi các ứng dụng web hiện đại.

Bạn có thể đọc thêm trong [tài liệu JSON](https://www.json.org/json-en.html).

Và đó là kết thúc tuần 9 ^^