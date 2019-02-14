---
layout: post
title: "Probability for Everyone[Math]"
---
In 1884, peirre-simon laplace wrote:

Probability theory is nothing but common sense reduced to calculation. ... [Probability] is thus simply a fraction whose numerator is the number of favorable cases and whose denominator is the number of all the cases possible ... when nothing leads us to expect that any one of these cases should occur more than any other.

Now, lets decode the vocubulary words:

*Trial*: A single occurence with an outcome that is uncertain until we observe it.
For example, rolling a single die.

*Outcome*: A possible result of a trial. One particular state of the world.
Example: rolling a single die
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

## Urn Problem

>Around 1700, Jacob Bernoulli wrote about removing colored balls from an urn in his landmark treatise [Ars Conjectandi](https://en.wikipedia.org/wiki/Ars_Conjectandi) and ever since then, explanations of probability relied on urn problems

For example, here is the three part problem adapted from mathforum.org:

	An urn contains 6 blue, 9 red, and 8 white balls. We select six balls at random. What is the probability of each of these outcomes:

	* All balls are red.

	* 3 are blue, and 1 is red, and 2 are white.

	* Exactly 4 balls are white.


We will start by defining the contents of the urn. A set can not contain multiple object that are equal to each other, so i will call the blue balls 'B1' through 'B6'.

```python
def balls(color, n):
    "A set of n numbered balls of the given color."
    return {color + str(i)
            for i in range(1, n + 1)}

urn = balls('B', 6) | balls('R', 9) | balls('W', 8)
urn
```

output: {'B1',
 'B2',
 'B3',
 'B4',
 'B5',
 'B6',
 'R1',
 'R2',
 'R3',
 'R4',
 'R5',
 'R6',
 'R7',
 'R8',
 'R9',
 'W1',
 'W2',
 'W3',
 'W4',
 'W5',
 'W6',
 'W7',
 'W8'}

Now we can define the sample space, U6, as the set of all 6-ball combinations.

```python
 U6 = combos(urn, 6)

random.sample(U6, 5)
```

output: ['W1 R4 W3 R7 R2 W7',
 'R3 W1 B6 W3 R2 W7',
 'R3 W5 B4 B2 W8 W7',
 'W2 B1 R3 B2 R8 B5',
 'B1 R5 W6 R9 R7 B5']



Define select such that select('R', 6) is the event of picking 6 red balls from the urn:

```python


def select(color, n, space=U6):
    "The subset of the sample space with exactly `n` balls of given `color`."
    return {s for s in space if s.count(color) == n}
```

Now We can answer the three questions:

P(select('R', 6), U6)

>Fraction(4, 4807)

P(select('B', 3)  & select('R', 1) & select('W', 2), U6)

>Fraction(240, 4807)

P(select('W', 4), U6)

>Fraction(350, 4807)







