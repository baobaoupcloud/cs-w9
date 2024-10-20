---
title : "JSON"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---
**JavaScript Object Notation (JSON)** is a text file of dictionaries with keys and values. This is a raw, computer-friendly way to get lots of data.

JSON is a very useful way of getting back data from the server.

You can see this in action in the `index.html` we examined together:

```html
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>shows</title>
    </head>
    <body>

        <input autocomplete="off" autofocus placeholder="Query" type="text">

        <ul></ul>

        <script>
            let input = document

.querySelector('input');
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

While the above may be somewhat cryptic, it provides a starting point for you to research **JSON** on your own to see how it can be implemented in your own web applications.

Further, we examined `app.py` to see how the JSON response is obtained:

```python
# Searches for shows using Ajax with JSON

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

Notice how `jsonify` is used to convert the result into a readable format acceptable by contemporary web applications.

You can read more in the [JSON documentation](https://www.json.org/json-en.html).

And that's the end of week 9 ^^