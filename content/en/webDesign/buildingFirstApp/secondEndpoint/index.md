---
title: A second endpoint
weight: 30
---

Let's add a second *endpoint*, as they're known, to our app:

```python{linenos=table, hl_lines=["8-10"]}
from flask import Flask
app = Flask(__name__)
 
@app.route('/')
def index():
    return 'Hello, Worldwww!'

@app.route('/goodbye')
def farewell():
    return 'Farewell, <em>stranger!</em>'

if __name__ == '__main__':
    app.run(debug=True)
```

As you can see, this defines a new URL pattern, and a new function to handle it.

Point your browser to [http://127.0.0.1:5000/goodbye](http://127.0.0.1:5000/goodbye) and see it in action.
You will see that the word stranger is in italics, because of the `<em>` tag we wrapped it in. If you go back to [http://127.0.0.1:5000/](http://127.0.0.1:5000/), you'll see that our greeting is still there.

Let's make it a bit more interesting, by making an endpoint which uses information in the URL pattern.

## More interesting patterns

```python{linenos=table, hl_lines=["12-14"]}
from flask import Flask
app = Flask(__name__)
 
@app.route('/')
def index():
    return 'Hello, Worldwww!'

@app.route('/goodbye')
def farewell():
    return 'Farewell, <em>stranger!</em>'

@app.route('/<greeting>/<person>')
def greeting(greeting, person):
    return f'{greeting}, <em>{person}!</em>'

if __name__ == '__main__':
    app.run(debug=True)
```

Add lines 12–14 above. Now your app will respond to URLs like these:
- [http://127.0.0.1:5000/Hello/Daisy](http://127.0.0.1:5000/Hello/Daisy)
- [http://127.0.0.1:5000/Goodbye/Bruce](http://127.0.0.1:5000/Goodbye/Bruce)

We can define a placeholder in a URL pattern with `<>`, like we did with `<greeting>` and `<person>`.
Flask will match URLs which look like that, and then feed the specific values into the function's arguments.
We can now use this information to help construct the page. In this case we're just printing it out, but when you visit Google or an online shop, these are used to tell the search engine what to search for, or the online store what product you want to view.
