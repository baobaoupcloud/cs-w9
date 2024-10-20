---
title : "Flask"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Flask

Flask là một thư viện bên thứ ba cho phép bạn lưu trữ các ứng dụng web bằng cách sử dụng framework Flask, một micro-framework trong Python.

Bạn có thể chạy Flask bằng cách thực thi lệnh `flask run` trong cửa sổ terminal của mình. Để thực hiện việc này, bạn cần có tệp `app.py` và một thư mục tên là `templates`.

#### Bắt đầu

1. Tạo một thư mục tên là `templates` và một tệp có tên `index.html` với nội dung sau:

    ```html
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta name="viewport" content="initial-scale=1, width=device-width">
            <title>hello</title>
        </head>
        <body>
            hello, {{ name }}
        </body>
    </html>
    ```

    Lưu ý rằng `{{ name }}` là một placeholder cho phần sẽ được cung cấp bởi server Flask sau này.

2. Trong cùng một thư mục với `templates`, tạo tệp `app.py`:

    ```python
    from flask import Flask, render_template, request

    app = Flask(__name__)

    @app.route("/")
    def index():
        name = request.args.get("name", "world")
        return render_template("index.html", name=name)
    ```

    Tệp `app.py` định nghĩa `app` như một ứng dụng Flask và xác định rằng route `/` sẽ trả về template `index.html` với đối số `name`. Nếu không có tên được cung cấp, nó sẽ mặc định là `"world"`.

3. Tạo một tệp `requirements.txt` với dòng sau:

    ```
    Flask
    ```

4. Chạy ứng dụng bằng lệnh `flask run` trong terminal của bạn.

#### Biểu mẫu

Để cải thiện trải nghiệm người dùng, bạn có thể tạo một biểu mẫu để người dùng nhập tên của họ. Cập nhật `index.html` như sau:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        <form action="/greet" method="get">
            <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
            <button type="submit">Greet</button>
        </form>
    </body>
</html>
```

Chỉnh sửa `app.py` để bao gồm một route mới:

```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/greet")
def greet():
    return render_template("greet.html", name=request.args.get("name", "world"))
```

Sau đó, tạo `greet.html`:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        hello, {{ name }}
    </body>
</html>
```

#### Layouts

Để tránh việc lặp lại mã code, bạn có thể tạo một layout cơ bản. Tạo `layout.html`:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>hello</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
```

Lưu ý rằng `{% block body %}{% endblock %}` cho phép chèn các mã khác từ các tệp HTML khác.

Cập nhật `index.html` và `greet.html` để mở rộng từ `layout.html`. Trước tiên, chỉnh sửa `index.html`:

```html
{% extends "layout.html" %}

{% block body %}
    <form action="/greet" method="get">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>
{% endblock %}
```

Lưu ý rằng dòng `{% extends "layout.html" %}` báo với server nơi để lấy layout của trang này. Sau đó, `{% block body %}{% endblock %}` cho biết đoạn mã nào sẽ được chèn vào `layout.html`.

Cuối cùng, chỉnh sửa `greet.html` như sau:

```html
{% extends "layout.html" %}

{% block body %}
    hello, {{ name }}
{% endblock %}
```

#### POST

Sử dụng `GET` có thể sẽ không an toàn trong một vài trường hợp, vì tên người dùng và mật khẩu sẽ hiển thị trong URL.  
Chúng ta có thể sử dụng phương thức `POST` để giải quyết vấn đề này bằng cách chỉnh sửa `app.py` như sau:

```python
# Chuyển sang POST

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/greet", methods=["POST"])
def greet():
    return render_template("greet.html", name=request.form.get("name", "world"))
```

Lưu ý rằng `POST` được thêm vào route `/greet`, và chúng ta sử dụng `request.form.get` thay vì `request.args.get`.  

Server sẽ tìm sâu hơn vào gói dữ liệu ảo và không hiển thị các mục trong `POST` trên URL.

Bạn có thể làm cho code này linh hoạt hơn bằng cách sử dụng một route duy nhất cho cả `GET` và `POST`. Để làm điều này, hãy sửa đổi `app.py` như sau:

```python
# Sử dụng một route duy nhất

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        return render_template("greet.html", name=request.form.get("name", "world"))
    return render_template("index.html")
```

Lưu ý rằng cả `GET` và `POST` đều được thực hiện trong một route duy nhất. Tuy nhiên, `request.method` được sử dụng để định hướng chính xác dựa trên loại yêu cầu mà người dùng gửi.

Theo đó, bạn có thể sửa đổi tệp `index.html` như sau:

```html
{% extends "layout.html" %}

{% block body %}

    <form action="/" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Tên" type="text">
        <button type="submit">Chào</button>
    </form>

{% endblock %}
```

Lưu ý rằng hành động của form đã được thay đổi.

Tuy nhiên, code này có một lỗi nhỏ. Với cách triển khai mới, khi ai đó không nhập tên vào form, nó sẽ hiển thị “Hello,” mà không có tên. Chúng ta có thể cải thiện code bằng cách chỉnh sửa `app.py` như sau:

```python
# Chuyển giá trị mặc định vào template

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        return render_template("greet.html", name=request.form.get("name"))
    return render_template("index.html")
```

Lưu ý rằng `name=request.form.get("name")` đã được thay đổi.

Cuối cùng, thay đổi `greet.html` như sau:

```html
{% extends "layout.html" %}

{% block body %}

    chào, {% if name %}{{ name }}{% else %}thế giới{% endif %}

{% endblock %}
```

Lưu ý rằng từ "chào" đã được thay đổi để cho phép một giá trị mặc định khi không có tên nào được xác định.


#### Flask và SQL

Flask có thể hoạt động với cơ sở dữ liệu SQL để lưu trữ và truy xuất dữ liệu. Điều này cho phép bạn tạo một ứng dụng web mà thông tin có thể tồn tại ngay cả khi server được khởi động lại.

Hãy cùng đi qua một ví dụ đơn giản về cách sử dụng Flask và SQL để tạo hệ thống đăng ký cơ bản, nơi người dùng có thể đăng ký tên và môn thể thao yêu thích của mình.

#### Bước 1: Cấu hình ứng dụng Flask với SQLite

Chúng ta sẽ sử dụng SQLite, một cơ sở dữ liệu nhẹ rất phù hợp cho các dự án đơn giản như thế này. Đầu tiên, hãy chắc chắn rằng bạn đã cài đặt các gói Python cần thiết.

Tạo một tệp `requirements.txt` và bao gồm nội dung sau:

```plaintext
Flask
cs50
```

Gói `cs50` bao gồm các hàm giúp tương tác dễ dàng hơn với cơ sở dữ liệu SQLite.

#### Bước 2: Tạo cơ sở dữ liệu

Trước khi tạo ứng dụng Flask, chúng ta hãy tạo cơ sở dữ liệu để lưu thông tin đăng ký người dùng. Để làm điều này, thực hiện các bước sau:

1. Trong terminal của bạn, chạy lệnh SQLite để tạo tệp cơ sở dữ liệu:

    ```bash
    sqlite3 mydatabase.db
    ```

2. Bên trong lệnh SQLite, tạo một bảng có tên là `registrants`:

    ```sql
    CREATE TABLE registrants (id INTEGER PRIMARY KEY, name TEXT, sport TEXT);
    ```

Lúc này sẽ tạo ra một bảng đơn giản với ba cột: `id` (tự động tăng cho mỗi người dùng mới), `name`, và `sport` (môn thể thao yêu thích).

#### Bước 3: Tạo ứng dụng Flask

Tiếp theo, chúng ta sẽ tạo một ứng dụng Flask cơ bản cho phép người dùng đăng ký tên và môn thể thao yêu thích của mình, sau đó xem tất cả các đăng ký.

Tạo tệp `app.py` như sau:

```python
from cs50 import SQL
from flask import Flask, render_template, request, redirect

# Cấu hình ứng dụng Flask
app = Flask(__name__)

# Kết nối với cơ sở dữ liệu SQLite
db = SQL("sqlite:///mydatabase.db")

# Danh sách các môn thể thao cho form
SPORTS = ["Bóng rổ", "Bóng đá", "Quần vợt"]

@app.route("/")
def index():
    return render_template("index.html", sports=SPORTS)

@app.route("/register", methods=["POST"])
def register():
    # Lấy dữ liệu từ form
    name = request.form.get("name")
    sport = request.form.get("sport")

    # Kiểm tra dữ liệu từ form nếu không có tên hoặc môn thể thao không hợp lệ, trả về trang thông báo lỗi:
    if not name or sport not in SPORTS:
        return render_template("failure.html")

    # Thêm người đăng ký vào cơ sở dữ liệu
    db.execute("INSERT INTO registrants (name, sport) VALUES (?, ?)", name, sport)

    # Chuyển hướng đến trang hiển thị danh sách người đăng ký
    return redirect("/registrants")

@app.route("/registrants")
def registrants():
    # Lấy tất cả người đăng ký từ cơ sở dữ liệu
    registrants = db.execute("SELECT * FROM registrants")

    # Hiển thị danh sách người đăng ký
    return render_template("registrants.html", registrants=registrants)
```


#### Bước 4: Tạo các template HTML

Bạn cần tạo ba tệp HTML cho ứng dụng này: `index.html`, `failure.html`, và `registrants.html`. Đặt những tệp này trong một thư mục có tên là `templates`.

##### `index.html` (Form đăng ký)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Đăng ký</h1>
    <form action="/register" method="post">
        <input name="name" placeholder="Tên" type="text">
        <select name="sport">
            <option disabled selected>Chọn một môn thể thao</option>
            {% for sport in sports %}
                <option value="{{ sport }}">{{ sport }}</option>
            {% endfor %}
        </select>
        <button type="submit">Đăng ký</button>
    </form>
{% endblock %}
```

##### `failure.html` (Trang thông báo lỗi)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Đăng ký không thành công</h1>
    <p>Hãy chắc chắn rằng bạn đã nhập tên hợp lệ và chọn một môn thể thao.</p>
{% endblock %}
```

##### `registrants.html` (Danh sách người đăng ký)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Người đăng ký</h1>
    <table>
        <thead>
            <tr>
                <th>Tên</th>
                <th>Môn thể thao</th>
            </tr>
        </thead>
        <tbody>
            {% for registrant in registrants %}
                <tr>
                    <td>{{ registrant.name }}</td>
                    <td>{{ registrant.sport }}</td>
                </tr>
            {% endfor %}
        </tbody>
    </table>
{% endblock %}
```

##### `layout.html` (Layout cơ bản cho tất cả các trang)

```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đăng ký</title>
</head>
<body>
    {% block body %}{% endblock %}
</body>
</html>
```

#### Bước 5: Chạy ứng dụng Flask

Trong terminal của bạn, chạy ứng dụng Flask:

```bash
flask run
```

Bây giờ, bạn có thể truy cập ứng dụng tại `http://127.0.0.1:5000/`. Khi bạn đăng ký một người dùng, tên và môn thể thao yêu thích của họ sẽ được lưu vào cơ sở dữ liệu và bạn có thể xem tất cả những người đăng ký trên trang **Người đăng ký**.