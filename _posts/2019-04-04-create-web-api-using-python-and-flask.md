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

>HTTP (Hypertext Transfer Protocol)

* It is the primary way to communicating data on the web.

>URL (Uniform Resource Locator)

* An address for a resource on the web

>JSON (JavaScript Object Notation)

* It is a text-based data storage format that is designed to be easy to read for both humans and machines

>REST (REpresentational State Transfer)

* It is a philosophy that describes some best practices for implementing APIs.

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

```python
python api.py
```

You should see output similar to this:

```python
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Follow the link above, [http://127.0.0.1:5000/](http://127.0.0.1:5000/)

![alt text](/images/api.jpg)


Congratulations, you’ve created a working web application!

## Creating the API

We’ll only be using GET requests in this tutorial, but many web applications need to use both GET requests (to send data from the application to the user) and POST requests (to receive data from a user).

First, we need to create some test data in the form of a list of dictionries.

```python
books = [
    {'id': 0,
     'title': 'A Fire Upon the Deep',
     'author': 'Vernor Vinge',
     'first_sentence': 'The coldsleep itself was dreamless.',
     'year_published': '1992'},
    {'id': 1,
     'title': 'The Ones Who Walk Away From Omelas',
     'author': 'Ursula K. Le Guin',
     'first_sentence': 'With a clamor of bells that set the swallows soaring, the Festival of Summer came to the city Omelas, bright-towered by the sea.',
     'published': '1973'},
    {'id': 2,
     'title': 'Dhalgren',
     'author': 'Samuel R. Delany',
     'first_sentence': 'to wound the autumnal city.',
     'published': '1975'}
]
```

and a route to return all the data.

```python
@app.route('/api/v1/resources/books/all', methods= ['GET'])

def api_all():
	return jsonify(books)

```

Run the code and visit [http://127.0.0.1:5000/api/v1/resources/books/all](http://127.0.0.1:5000/api/v1/resources/books/all) to view the data



