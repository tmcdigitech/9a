---
title: Templates with parameters
weight: 60
---
Now that we have a template, it would be great if we could change little bits of it without having to make a whole new template. And we can.

Let's make a really short template to highlight the idea.

Here is the file structure for our project:

```
📂 flask_demo
 ├─📄 app.py
 └─📂 templates
    └─📄 base.html
```

And here are the files:

### `app.py`
```python{linenos=table}
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def index():
    c = 'I am a boring web server!'
    return render_template('base.html',content=c)

@app.route('/about')
def about():
    c = 'This is the about page.'
    return render_template('base.html',content=c)

@app.route('/faq')
def faq():
    c = 'If there were any frequently asked questions, they\'d be answered on this page.'
    return render_template('base.html',content=c)

if __name__ == '__main__':
    app.run(debug=True)
```

### `templates/base.html`
```html
<a href="/">[ Home ]</a>
<a href="/about">[ About ]</a>
<a href="/faq">[ FAQ ]</a>

<h1>A very basic site</h1>
<hr />

{{ content }}
```

When you load the page, you'll see that there is now a menu bar across the top of each page, provided by the template. The part below the line is passed in to the template by our functions. If you look in app.py, each one calls `render_template`, tells it which template to use, and then defines the value of the variable `content`, which is rendered in the template. The double braces, `{{ }}`, are the way to tell the templating engine, Jinja, to print out a python *expression* such as a variable.

## Template protection
Try adding HTML tags to the string that you pass to the template, e.g. change line 6 of app.py to read:

```python{linenos=table,linenostart=6}
    c = 'I <em>am</em> a boring web server!'
```

and reload the page. You will notice that the browser displays the tags, rather than rendering them. If you look at the source code of the page, you'll notice that the template engine quietly changed your text to read:

```HTML
<a href="/">[ Home ]</a>
<a href="/about">[ About ]</a>
<a href="/faq">[ FAQ ]</a>

<h1>A very basic site</h1>
<hr />

I &lt;em&gt;am&lt;/em&gt; a boring web server!
```

The pattern `&name;`, i.e. a word flanked by an ampersand and a semicolon is the way to display characters that:
- have magic meanings in HTML, such as &lt;, &gt; and &amp;; or

- are traditionally hard to enter using your keyboard, such as `&deg;` &deg;, `&rarr;` &rarr; and `&euro;` &euro;.

You can also give the id for any Unicode character, which means you can print things like `&#128169;` &#128169;.

In our case here, Jinja deliberately *escapes* any magic HTML characters so your strings are free of HTML, which means that they won't stuff up your formatting by mistake. This is particularly a problem if you display text straight from a user. It is possible to turn it off, but you should be able to do what you need to do without ever disabling the safety mechanisms in Flask and Jinja.
