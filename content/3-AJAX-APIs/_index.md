---
title : "AJAX and APIs"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
**Asynchronous JavaScript and XML** (AJAX) is a combination of web application development technologies that make web applications more responsive to user interaction. Whenever your users interact with a web application, such as when they click buttons or checkmark boxes, the browser exchanges data with the remote server.

An **Application Programming Interface (API)** is a series of specifications that allow you to interface with another service. For example, we could utilize **IMDB’s API** to interface with their database. We might even integrate APIs for handling specific types of data downloadable from a server.

Improving upon shows, looking at an improvement of `app.py`, we saw the following:

```python
# Searches for shows using Ajax

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

Notice that the search route executes a SQL query.

Looking at `search.html`, you’ll notice that it is very simple:

```html
{% for show in shows %}
    <li>{{ show["title"] }}</li>
{% endfor %}
```

Notice that it provides a bulleted list.

Finally, looking at `index.html`, notice that **AJAX** code is utilized to power the search:

```html
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>shows</title>
    </head>
    <body>

        <input autocomplete="off" autofocus placeholder="Query" type="search">

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

Notice an event listener is utilized to dynamically query the server to provide a list that matches the title provided. This will locate the `ul` tag in the HTML and modify the web page accordingly to include the list of the matches.