---
title : "Session"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
#### Session

While the above code is useful from an administrative standpoint, where a back-office administrator could add and remove individuals from the database, one can imagine how this code is not safe to implement on a public server.

For one, bad actors could make decisions on behalf of other users by hitting the deregister button – effectively deleting their recorded answer from the server.  
Web services like Google use login credentials to ensure users only have access to the right data.

We can actually implement this using **cookies**. Cookies are small files that are stored on your computer, such that your computer can communicate with the server and effectively say, “I’m an authorized user that has already logged in.” This authorization through this cookie is called a **session**.

In the simplest form, we can implement this by creating a folder called `login` and then adding the following files.

First, create a file called `requirements.txt` that reads as follows:

```plaintext
Flask
Flask-Session
```

Notice that in addition to **Flask**, we also include **Flask-Session**, which is required to support login sessions.

Second, in a `templates` folder, create a file called `layout.html` that appears as follows:

```html
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>login</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
```

Notice this provides a very simple layout with a title and a body.

Third, create a file in the `templates` folder called `index.html` that appears as follows:

```html
{% extends "layout.html" %}

{% block body %}

    {% if name %}
        You are logged in as {{ name }}. <a href="/logout">Log out</a>.
    {% else %}
        You are not logged in. <a href="/login">Log in</a>.
    {% endif %}

{% endblock %}
```

Notice that this file looks to see if `session["name"]` exists (elaborated further in `app.py` below). If it does, it will display a welcome message. If not, it will recommend you browse to a page to log in.

Fourth, create a file called `login.html` and add the following code:

```html
{% extends "layout.html" %}

{% block body %}

    <form action="/login" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Log In</button>
    </form>

{% endblock %}
```

Notice this is the layout of a basic login page.

Finally, create a file called `app.py` and write code as follows:

```python
from flask import Flask, redirect, render_template, request, session
from flask_session import Session

# Configure app
app = Flask(__name__)

# Configure session
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

Notice the modified imports at the top of the file, including `session`, which will allow you to support sessions. Most importantly, notice how `session["name"]` is used in the login and logout routes. The login route will assign the login name provided and assign it to `session["name"]`. However, in the logout route, the logging out is implemented by clearing the value of the session.
