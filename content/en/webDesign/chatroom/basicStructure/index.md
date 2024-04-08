---
title: Basic structure
weight: 10
---

We'll need:
- an index (home) page, which welcomes people and directs them to log in to the chat room.
- a login form and handler.
- a page for the chat room itself, with a form field for chatting.
- a template to hold everything together
- some styling, maybe?
- some way of storing the chat log

Let's start with some basic structure:
```
📂 chatroom
 ├─📄 app.py
 ├─📄 app_config.py
 ├─📂 static
 │  └─📄 main.css
 └─📂 templates
    ├─📄 base.html
    ├─📄 chat.html
    ├─📄 index.html
    └─📄 login.html
```

### `app.py`
```python
from flask import Flask, render_template
import app_config

app = Flask(__name__)
app.config.from_object(app_config)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/login')
def login():
    return render_template('login.html')

@app.route('/chat')
def chat():
    return render_template('chat.html')

if __name__ == '__main__':
    app.run(host=app_config.HOST,port=app_config.PORT, debug=app_config.DEBUG_MODE)
```

### `app_config.py`
```python
DEBUG_MODE = True
HOST = '127.0.0.1'
PORT = 8000
```

### `static/main.css`
```css
@import url('https://fonts.googleapis.com/css2?family=Ubuntu:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&display=swap');

body {
    font-family: "Ubuntu", sans-serif;
}
```

### `templates/base.html`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blathr | {% block title %}:-){% endblock %}</title>
    <link rel="stylesheet" href="static/main.css">
  </head>
  <body>
    <h1>Blathr <span style="color: 888;">— a simple chat service</span></h1>
    <a href="/">[ Home ]</a>
    <a href="/login">[ Start ]</a>
    <a href="/chat">[ Chat ]</a>
    <hr/>
    {% block content %}
    {% endblock %}
  </body>
</html>
```

### `templates/chat.html`
```html
{% extends 'base.html' %}
{% block content %}
<p>This is the chat room for Blathr.
Chat log and somewhere to type are on the way!</p>
{% endblock %}
```

### `templates/index.html`
```html
{% extends 'base.html' %}
{% block content %}
<p>This is the index page for Blathr.
There'll be some welcoming
writing here at some point...</p>
{% endblock %}
```

### `templates/login.html`
```html
{% extends 'base.html' %}
{% block content %}
<p>This is the login page for Blathr.
Form to come...</p>
{% endblock %}
```
