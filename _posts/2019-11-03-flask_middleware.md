---
layout: post
title: Flask Middleware Small Note
author: Iurii Ivanov
tags: [flask, uwsgi, middleware]
---

I had to add a middleware to Flask application once. This is how it was done ...

Middleware is a specific layer to mutate a request before it gets to the view,
it is jsut a piece of code which is called automatically every time a requests comes in the server.
You can add any amount of layers, they will be executed consequently, in specific order (does not matter for now).
It can be used to do something with client session, check if user is logged in ot smth, mutate request object,
logging and so on.

You just have to difine the class like that:

```python
from werkzeug.wrappers import Request

class Middleware:
    def __init__(self, app):
        self.app = app

    def __call__(self, environ, start_response, *args, **kwargs):
        request = Request(environ)
        
        # IMPLEMENT YOUR LOGIC HERE 
        
        return self.app(environ, start_response)
```

`environ` is the WSGI “environment” and `start_response` is the WSGI callable that is used to start the response phase.
The Request class wraps the environ for easier access to request variables (form data, request headers etc.).

To enable new middleware just wrap/register your Flask app with it:

```python
app = Flask(__name__)
app.wsgi_app = middleware.SimpleMiddleWare(app.wsgi_app)
```

*NOTE:* This staff can be done using Python decorators. But in this case you have to add decorator to each method/function/view
you want to apply the logic.
