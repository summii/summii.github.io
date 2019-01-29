---
layout: post
title: "Probability for Everyone"
date: 2019-01-29
---

In 1884, peirre-simon laplace wrote:

Probability theory is nothing but common sense reduced to calculation. ... [Probability] is thus simply a fraction whose numerator is the number of favorable cases and whose denominator is the number of all the cases possible ... when nothing leads us to expect that any one of these cases should occur more than any other.

Now, lets decode the vocubulary words:

*Trial*: A single occurence with an outcome that is uncertain until we observe it.

*Outcome*: A possible result of a trial. One particular state of the world.
Example: 7

*Sample Space*: The set of all possible outcomes for the trial.
For example: {1,2,3,4,5,6}

*Event*: A subset of outcomes that together have some property we are interested in.
For example: the event "odd die roll" is the set of outcomes {3,6}

*Probability*: Number of favorable cases in a simple space divided by the "number of all the cases in the sample space".

Let's implement something using python.

```
from fractions import Fraction 

def P(event, space):
	return(cases(favorable(event, space)),
		cases(space))

favorable = set.intersection

cases = len

D = {1,2,3,4,5,6}  # a sample space

even = { 2  , 4  , 6 }  # a event

prime = {2, 3, 5, 7, 11, 13}
odd   = {1, 3, 5, 7, 9, 11, 13}

print(P(even,D)) 
output: (1,2)

print(P(odd, D))
output: (1,2)

print(P((even | prime), D)) # The probability of an even or prime die roll
output: (5, 6)
print(P((odd & prime), D))  # The probability of an odd prime die roll
output: (1,3)

```

