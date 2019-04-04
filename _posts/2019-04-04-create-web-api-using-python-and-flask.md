---
layout: post
title: "Web API using python and flask"
---


### What is an API?

Web APIs are the tools for making information and application functionality accesible over the internet.

## When to create an API

* Your data set is large and making download via FTP is difficult.
* Your user need to access the data in real time as a part of their application

If you have data that you want share with others, an API is one way to do it. However, APIs are not the best way of sharing the data with others. If the size of data you are providing is very small, it is better to provide them "data dump" in the form of JSON, XML, CSV or API as other option.


## API Terminology

* HTTP (Hypertext Transfer Protocol)

> It is the primary way to communicating data on the web.

* URL (Uniform Resource Locator)

> An address for a resource on the web

* JSON (JavaScript Object Notation)

> iT is a text-based data storage format that is designed to be easy to read for both humans and machines

* REST (REpresentational State Transfer)

>It is a philosophy that describes some best practices for implementing APIs.

## Implementing API

This section will show you how to build API using python and flask web framework.

In macOS, you can create a project folder using this command

```python
mkdir api
cd api

```

Run the following commands to install the required packages

```python

pip install flask flask-jsonpify flask-sqlalchemy flask-restful

```

Next, open your text editor and enter the following code

```python

import flask

app = flask.Flask(__name__)
app.config["DEBUG"] = True


@app.route('/', methods=['GET'])
def home():
    return "<h1>Building API Prototype</h1><p>This is random text to test random things</p>"

app.run()
```

Run the flask application with the following command

>python api.py

You should see output similar to this:

>* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

