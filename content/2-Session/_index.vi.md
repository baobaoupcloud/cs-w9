---
title : "Phiên"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Phiên (Sessions)

Mã này có thể sẽ không an toàn khi triển khai trên một server công khai. Lý do là các tác nhân xấu có thể thực hiện các hành động thay cho người dùng khác, ví dụ như xóa câu trả lời của họ từ server. 

Các dịch vụ web như Google sử dụng thông tin đăng nhập để đảm bảo chỉ những người dùng có thẩm quyền mới được truy cập dữ liệu cần thiết.

Chúng ta có thể thực hiện điều này bằng cách sử dụng **cookie**. Cookie là những tệp nhỏ được lưu trữ trên máy tính của bạn, giúp máy tính của bạn giao tiếp với server và thông báo rằng, "Tôi là một người dùng đã đăng nhập hợp lệ." Sự xác thực thông qua cookie này được gọi là **phiên (session)**.

Ví dụ, chúng ta có thể thực hiện điều này bằng cách tạo một thư mục có tên là `login` và thêm các tệp sau.

Đầu tiên, tạo tệp `requirements.txt` với nội dung sau:

```plaintext
Flask
Flask-Session
```

Lưu ý rằng ngoài **Flask**, chúng ta còn bao gồm **Flask-Session** để hỗ trợ các phiên đăng nhập.

Thứ hai, trong thư mục `templates`, tạo một tệp có tên `layout.html` như sau:

```html
<!DOCTYPE html>

<html lang="vi">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>Đăng nhập</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
```

Đây là một layout đơn giản với tiêu đề và phần thân.

Thứ ba, tạo một tệp trong thư mục `templates` đặt tên là `index.html` với nội dung như sau:

```html
{% extends "layout.html" %}

{% block body %}

    {% if name %}
        Bạn đã đăng nhập với tên {{ name }}. <a href="/logout">Đăng xuất</a>.
    {% else %}
        Bạn chưa đăng nhập. <a href="/login">Đăng nhập</a>.
    {% endif %}

{% endblock %}
```

Tệp này kiểm tra xem `session["name"]` có tồn tại không (được giải thích thêm trong `app.py` bên dưới). Nếu có, nó sẽ hiển thị thông báo chào mừng. Nếu không, nó sẽ đề nghị bạn chuyển đến trang đăng nhập.

Thứ tư, tạo một tệp có tên là `login.html` và thêm mã sau:

```html
{% extends "layout.html" %}

{% block body %}

    <form action="/login" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Tên" type="text">
        <button type="submit">Đăng nhập</button>
    </form>

{% endblock %}
```

Đây là giao diện cơ bản của trang đăng nhập.

Cuối cùng, tạo tệp `app.py` và viết mã như sau:

```python
from flask import Flask, redirect, render_template, request, session
from flask_session import Session

# Cấu hình ứng dụng
app = Flask(__name__)

# Cấu hình session
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)

@app.route("/")
def index():
    return render_template("index.html", name=session.get("name"))

@app.route("/login", methods=["GET", "POST"])
def login():
    if request.method == "POST":
        session["name"] = request.form.get("name")
        return redirect("/")
    return render_template("login.html")

@app.route("/logout")
def logout():
    session.clear()
    return redirect("/")
```

Chúng ta đã thêm `session` trong các imports ở đầu tệp, điều này cho phép bạn hỗ trợ các phiên làm việc. Quan trọng nhất, `session["name"]` được sử dụng trong các route đăng nhập và đăng xuất. Route đăng nhập sẽ gán tên đăng nhập mà người dùng cung cấp vào `session["name"]`. Tuy nhiên, trong route đăng xuất, việc đăng xuất được thực hiện bằng cách xóa dữ liệu của phiên.