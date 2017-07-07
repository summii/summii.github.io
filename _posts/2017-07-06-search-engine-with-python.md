---
layout: post
title: "Build Basic Web Search Engine Using Python - Part 1"
date: 2017-07-06
---

Getting Setup

We're going to use python 2.7.If you don't have python 2.7, you need to download a proper version from <a href="https://www.python.org/download/releases/2.7.3/">here</a> 

I assume that you know basics of python, otherwise you can brush-up your skill [here]("https://docs.python.org/2/tutorial/index.html"). 

# Finding your data

For this example, we're going to use [xkcd](https://xkcd.com/353/) webpage. Go ahead and browse it. If you right click on the page, one of the option you see "view page source" and when you click on that what you see is source code. What is important for us is link,here's a example of links

![alt text](/img/link.png "xkcd page source")

# Planning your code
Our goal is to take the text that came back from a web request, find link in that text, which is gonna be tag that start with *<a href=\"<url>\"*(Not all web pages have the same structure) and then extract from that tag the url of the web page that it links to. So those are *URLS*  we're going to use in our crawler to make progress.




.......................in process
