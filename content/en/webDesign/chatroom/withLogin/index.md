---
title: Logging in
weight: 20
---

### `app.py`
```python
from flask import Flask, render_template, request
import app_config

app = Flask(__name__)
app.config.from_object(app_config)

@app.route('/')
def index():
    return render_template('index.html')

@app.route("/login", methods = ['GET', 'POST'])
def login():
    if request.method=='GET':
        return render_template('login.html')
    dn = request.form['displayName']
    pw = request.form['password']
    return f"You logged in as {dn} with a password of {pw}"

@app.route('/nochat')
def chat():
    return render_template('chat.html')

if __name__ == '__main__':
    app.run(host=app_config.HOST,port=app_config.PORT, debug=app_config.DEBUG_MODE)
```

### `templates/login.html`
```html
{% extends 'base.html' %}
{% block content %}
<p>This is the login page for Blathr.
Form to come...</p>

<form target="/login" method="POST">
    <label for="displayName">Display name</label>
    <input type="text" id="displayName" name="displayName" value="" placeholder="What do you want to call yourself?"/>
    <br/>
    <label for="password">Password</label>
    <input type="password" id="password" name="password" value="" placeholder="What is your secret word?"/>
    <br/>
    <input type="submit" name="login" value="Login"/>
</form>
{% endblock %}
```
