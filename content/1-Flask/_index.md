---
title : "Flask"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
#### Flask

Flask is a third-party library that allows you to host web applications using the Flask framework, a micro-framework within Python. 

You can run Flask by executing `flask run` in your terminal window. To do this, you'll need an `app.py` file and a folder called `templates`.

#### Getting Started

1. Create a folder called `templates` and a file named `index.html` with the following content:

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

    Notice the `{{ name }}` is a placeholder for something that will be provided by the Flask server later.

2. In the same folder as `templates`, create an `app.py` file:

    ```python
    from flask import Flask, render_template, request

    app = Flask(__name__)

    @app.route("/")
    def index():
        name = request.args.get("name", "world")
        return render_template("index.html", name=name)
    ```

    The `app.py` file defines `app` as the Flask application and specifies that the `/` route returns the `index.html` template with the `name` argument. If no name is provided, it defaults to `"world"`.

3. Create a `requirements.txt` file with the following line:

    ```
    Flask
    ```

4. Run the application using the command `flask run` in your terminal.

#### Forms

To improve the user experience, you can create a form for users to submit their name. Update `index.html` as follows:

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

Modify `app.py` to include a new route:

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

Then, create `greet.html`:

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

To avoid repeating code, you can create a base layout. Create `layout.html`:

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
Notice that the `{% block body %}{% endblock %}` allows for the insertion of other code from other HTML files.

Update `index.html` and `greet.html` to extend `layout.html`. First, modify the `index.html`:

```html
{% extends "layout.html" %}

{% block body %}
    <form action="/greet" method="get">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>
{% endblock %}
```
Notice that the line `{% extends "layout.html" %}` tells the server where to get the layout of this page. Then, the `{% block body %}{% endblock %} tells `what code to be inserted into `layout.html`.

Finally, edit `greet.html` as follow:
```html
{% extends "layout.html" %}

{% block body %}
    hello, {{ name }}
{% endblock %}
```


#### POST
You can imagine scenarios where it is not safe to utilize `GET`, as usernames and passwords would show up in the URL.  
We can utilize the method `POST` to help with this problem by modifying `app.py` as follows:

```python
# Switches to POST

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/greet", methods=["POST"])
def greet():
    return render_template("greet.html", name=request.form.get("name", "world"))
```

Notice that `POST` is added to the `/greet` route, and that we use `request.form.get` rather than `request.args.get`.  

This tells the server to look deeper in the virtual envelope and not reveal the items in `POST` in the URL.  
Still, this code can be advanced further by utilizing a single route for both `GET` and `POST`. To do this, modify `app.py` as follows:

```python
# Uses a single route

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        return render_template("greet.html", name=request.form.get("name", "world"))
    return render_template("index.html")
```

Notice that both `GET` and `POST` are done in a single routing. However, `request.method` is utilized to properly route based upon the type of routing requested by the user.

Accordingly, you can modify your `index.html` as follows:

```html
{% extends "layout.html" %}

{% block body %}

    <form action="/" method="post">
        <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
        <button type="submit">Greet</button>
    </form>

{% endblock %}
```

Notice that the form action is changed.

Still, there is a bug in this code. With our new implementation, when someone types in no name into the form, "Hello," is displayed without a name. We can improve our code by editing `app.py` as follows:

```python
# Moves default value to template

from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        return render_template("greet.html", name=request.form.get("name"))
    return render_template("index.html")
```

Notice that `name=request.form.get("name")` is changed.

Finally, change `greet.html` as follows:

```html
{% extends "layout.html" %}

{% block body %}

    hello, {% if name %}{{ name }}{% else %}world{% endif %}

{% endblock %}
```

Notice how "hello," is changed to allow for a default output when no name is identified.


#### Flask and SQL

Flask can work with a SQL database to store and retrieve data. This allows you to create a web app where information can persist even when the server restarts.

Let’s walk through a simple example of how you can use Flask and SQL to create a basic registration system where users can register their names and favorite sports.

#### Step 1: Set Up Your Flask App with SQLite

We’ll use SQLite, a lightweight database that is great for simple projects like this. First, make sure you install the necessary Python packages.

Create a `requirements.txt` file and include the following:

```plaintext
Flask
cs50
```

The `cs50` package includes functions that make it easier to interact with an SQLite database.

#### Step 2: Create the Database

Before creating the Flask app, let's create a database where we’ll store user registrations. To do this, follow these steps:

1. In your terminal, run the SQLite command to create a database file:

    ```bash
    sqlite3 mydatabase.db
    ```

2. Inside the SQLite prompt, create a table called `registrants`:

    ```sql
    CREATE TABLE registrants (id INTEGER PRIMARY KEY, name TEXT, sport TEXT);
    ```

This creates a simple table with three columns: `id` (which will automatically increment for each new user), `name`, and `sport`.

#### Step 3: Create the Flask App

Next, we’ll create a basic Flask app that allows users to register their name and favorite sport, and then view all the registrations.

Here’s how the `app.py` file might look:

```python
from cs50 import SQL
from flask import Flask, render_template, request, redirect

# Configure Flask app
app = Flask(__name__)

# Connect to the SQLite database
db = SQL("sqlite:///mydatabase.db")

# List of sports for the form
SPORTS = ["Basketball", "Soccer", "Tennis"]

@app.route("/")
def index():
    return render_template("index.html", sports=SPORTS)

@app.route("/register", methods=["POST"])
def register():
    # Get the data from the form
    name = request.form.get("name")
    sport = request.form.get("sport")

    # Validate the form data
    if not name or sport not in SPORTS:
        return render_template("failure.html")

    # Insert the registrant into the database
    db.execute("INSERT INTO registrants (name, sport) VALUES (?, ?)", name, sport)

    # Redirect to the registrants page
    return redirect("/registrants")

@app.route("/registrants")
def registrants():
    # Get all registrants from the database
    registrants = db.execute("SELECT * FROM registrants")

    # Display the registrants
    return render_template("registrants.html", registrants=registrants)
```

#### Step 4: Create the HTML Templates

You need three HTML files for this simple app: `index.html`, `failure.html`, and `registrants.html`. Put these inside a folder called `templates`.

##### `index.html` (The Registration Form)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Register</h1>
    <form action="/register" method="post">
        <input name="name" placeholder="Name" type="text">
        <select name="sport">
            <option disabled selected>Select a sport</option>
            {% for sport in sports %}
                <option value="{{ sport }}">{{ sport }}</option>
            {% endfor %}
        </select>
        <button type="submit">Register</button>
    </form>
{% endblock %}
```

##### `failure.html` (Error Page)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Registration Failed</h1>
    <p>Make sure you entered a valid name and selected a sport.</p>
{% endblock %}
```

##### `registrants.html` (List of Registrants)

```html
{% extends "layout.html" %}

{% block body %}
    <h1>Registered Users</h1>
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Sport</th>
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

##### `layout.html` (Base Layout for All Pages)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration</title>
</head>
<body>
    {% block body %}{% endblock %}
</body>
</html>
```

#### Step 5: Run the Flask App

In your terminal, run the Flask app:

```bash
flask run
```

You can now access the app at `http://127.0.0.1:5000/`. When you register a user, their name and sport will be saved to the database, and you can view all the registrants on the **Registered Users** page.
