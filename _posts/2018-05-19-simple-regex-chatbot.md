---
layout: post
title: "Simple Chatbot Using Regular Expressions"
date: 2018-05-19
---

In this post I will use python module **re** to build simple chatbot. It won't be very capable and it will require lot of "hard coding" of all the ways people may try 
to say something. This is a very controlled approach that was common before moder chatbot techniques were developed.

Let's write a regular expressions to recognize several different human greetings at the start of conversation.

```python
>>> import re
>>> re_greeting = re.compile(r"[^a-z]*([y]o|[h']?ello|ok|hey|(good[ ])?(morn[gin']{0,3}|afternoon|even[gin']{0,3}))[\s,;:]{1,3}([a-z]{1,20})", flags=re.IGNORECASE)
>>> re_greeting.match('Hello Rosa')
<_sre.SRE_Match object; span=(0, 10), match='Hello Rosa'>
>>> re_greeting.match('Hello Rosa').groups()
('Hello', None, None, 'Rosa')
>>> re_greeting.match("Good morning Rosa")
<_sre.SRE_Match object; span=(0, 17), match="Good morning Rosa">
>>> re_greeting.match("Good Norning Rosa")
>>> re_greeting.match("Good Morn'n Rosa")
<_sre.SRE_Match object; span=(0, 16), match="Good Morn'n Rosa">
>>> re_greeting.match("yo Rosa")
<_sre.SRE_Match object; span=(0, 7), match='yo Rosa'>
```

It will work for suprising range of greetings but missed that "Norning" typo. This is reason NLP is really hard . This mean that our regular expression is too strict or too loose.




```python
>>> my_names = set(['rosa', 'rose', 'chatty', 'chatbot', 'bot', 'chatterbot'])
>>> curt_names = set(['hal', 'you', 'u'])
>>> greeter_name = None  # we don't yet know who is chatting to the bot

>>> match = re_greeting.match(input())

>>> if match:
	     at_name = match.groups()[-1]
	     if at_name in curt_names:
	        print("Good one.")
	     elif at_name.lower() in my_names:
	         print("Hi {}, How are you?".format(greeter_name or '')
```


# In progress...............