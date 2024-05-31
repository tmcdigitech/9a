---
title: Final version
weight: 100
---
```
📂 Blathr/
├── 📄 app.py
├── 📄 chat.json
├── 📂 static/
│   └── 📄 base.css
└── 📂 templates/
    ├── 📄 base.html
    ├── 📄 chat.html
    └── 📄 login.html
```

### `app.py`
```python
from flask import Flask, render_template, request, session, redirect, url_for, send_from_directory
from datetime import datetime
import json
import os

app = Flask(__name__)
app.secret_key = 'slbo3i4k5uytf,ib4ku5w'

@app.template_filter('date')
def datetime_format(datestr, format=('%-d %b')):
    d = datetime.strptime(datestr,'%Y-%m-%d %H:%M:%S')
    return d.strftime(format)

@app.route('/')
def index():
    return redirect(url_for('chat'))

@app.route('/chat', methods=['get','post'])
def chat():
    if not session or 'uname' not in session:
        return redirect(url_for('login'))

    # Load posts from file
    with open("chat.json","r") as posts_file:
        posts = json.load(posts_file)
        posts_file.close()
    
    if request.method=="POST":
        # Save their new post
        newPost = {'uname': session['uname'], 'dname': session['dname'], 'time': datetime.now().strftime('%Y-%m-%d %H:%M:%S'), 'post': request.form['post']}
        posts.append(newPost)
        # Save posts to file
        with open("chat.json","w") as posts_file:
            json.dump(posts, posts_file, indent=4)
            posts_file.close()
    return render_template('chat.html', session=session, posts=reversed(posts))
 
@app.route('/login', methods=['get','post'])
def login():
    if session and 'uname' in session:
        redirect(url_for('chat'))
    if request.method=="GET":
        return render_template('login.html')
    session['uname'] = request.form['username']
    session['dname'] = request.form['display_name']
    return redirect(url_for('index'))

# IGNORE THIS BIT
@app.route('/src/')
def src_list():
    s = ''
    for root, dirs, files in os.walk("."):
        for name in files:
            p = os.path.join(root, name)
            s+= f'<a href="/src/{p}">{p}</a><br/>\n'
        # for name in dirs:
        #     p = os.path.join(root, name)
        #     s+= "    "*level+p+"<br/>"
            # s+= src_tree(p,level+1)
    return s

if __name__ == '__main__':
    app.run(debug=True)
```

### `chat.json`
```json
[]
```

### `static/base.css`
```css
.postDname {
    color: green;
}
.postText {
    color: blue;
}
```

### `templates/base.html`
```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="color-scheme" content="light dark" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css" />
    <link rel="stylesheet" href="/static/base.css" />
    <title>Hello world!</title>
  </head>
  <body>
    <main class="container">
        <h1>Blathr</h1>
        {% if session['uname'] %}
        <p>Hello, {{ session['dname'] }} ({{ session ['uname'] }})</p>
        {% endif %}
        {% block content %}
        {% endblock %}
    </main>
  </body>
</html>
```

### `templates/chat.html`
```html
{% extends 'base.html' %}
{% block content %}
<form action="/chat" method="post">
    <fieldset>
      <label>
        <input
          type="text"
          name="post"
          placeholder="Chat here…"
        />
      </label>
    </fieldset>
  
    <input
      type="submit"
      value="Post"
    />
</form>

{% for post in posts %}
<p>
  <span class="postDname">{{ post['dname'] }}</span><br/>
  <span class="postText">{{ post['post'] }}</span><br/>
  <span class="postTime">{{ post['time'] | date('%H:%M')}}</span>
</p>
{% endfor %}
{% endblock %}
```

### `templates/login.html`
```html
{% extends 'base.html' %}
{% block content %}
<form action="/login" method="post">
    <fieldset>
      <label>
        Username
        <input
          type="text"
          name="username"
          placeholder="e.g. turbowizard42"
        />
      </label>
      <label>
        Password
        <input type="password" name="password" placeholder="Password" autocomplete="password" />
      </label>
      <label>
        Display name
        <input
          type="text"
          name="display_name"
          placeholder="e.g. Turbo Wizard"
        />
      </label>
    </fieldset>
  
    <input
      type="submit"
      value="Login"
    />
</form>
{% endblock %}
```

