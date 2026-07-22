Exercises

As usual, don't run the code. Build the answer from the mental model.

Exercise 1 — What Is a Type?

In your own words:

What is a type?
Is a type the same thing as an object?
Does a type store an object's data?
What does a type actually define?
Exercise 2 — Object vs Type

Consider these objects conceptually:

5

10

100

Without running anything, answer:

How many objects exist?
Do they all contain the same data?
Why do they all behave the same way?
Where does that shared behavior come from?
Exercise 3 — Different Types

Conceptually compare:

42

"42"

[42]

Explain:

Why are these three completely different kinds of objects?
Why does Python allow different operations on each?
What determines those operations?
Is the difference caused by the names or by something deeper?
Exercise 4 — AI Engineering Thinking

Suppose an AI framework creates one million tensor objects during training.

Conceptually explain:

Why doesn't each tensor need its own copy of all tensor operations?
What is shared between all tensor objects?
Why is this design more memory-efficient?
How does this relate to Python's idea of types?
