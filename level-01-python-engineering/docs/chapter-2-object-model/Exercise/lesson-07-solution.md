# Exercises
## Exercise 1

In your own words:

Why does Python cache small integers?

Why is this optimization useful?

Why does Python cache them? Numbers from -5 to 256 are incredibly common in programming (used for loops, indices, and flags). Pre-allocating them saves Python from constantly creating and destroying the same numbers.

Why is this optimization useful? It speeds up execution by avoiding expensive memory allocations. It also reduces overall memory fragmentation

## Exercise 2

Suppose:

a = 5
b = 5
c = 5

Conceptually draw the memory using ASCII.

Answer:

How many integer objects exist?
How many names exist?
What is the reference count of the integer 5 (ignoring Python's internal references)?

        5
      / | \
     /  |  \
    a   b   c

How many integer objects exist? Exactly 1 object.

How many names exist? There are 3 names (a, b, and c).

What is the reference count? 3

## Exercise 3

Suppose:

a = 1000
b = 1000

Without running the code:

Is Python required to make a and b the same object?
Are they guaranteed to be equal?
Why is using is here unreliable?

Is Python required to make them the same object? No. The language specification does not require caching for numbers outside the -5 to 256 range.

Are they guaranteed to be equal? Yes. Their values are identical (a == b is True) but their object is not guaranteed to be equal.

Why is is unreliable here? is checks memory addresses, not values. Python might create two distinct objects or optimize them into one. You cannot rely on it.

## Exercise 4

Why is small integer caching only possible because integers are immutable?

Imagine integers were mutable. What kinds of bugs would occur if millions of variables shared the same integer object?

Why is it only possible because they are immutable? Because integers cannot be changed, it is completely safe for millions of variables to share one object. No variable can alter the value for the others.

What bugs would occur if integers were mutable? If you changed the value of a variable x = 5 to 6, every single 5 in the entire program would suddenly become a 6. Loop counters, array indices, and math operations across your codebase would instantly break


## Exercise 5 (Thinking)

Suppose Python cached every integer ever created.

Think about a web server that runs continuously for months.

What problems would this create regarding:

memory usage,
scalability,
performance?

Memory Usage: Memory would leak continuously. Every large unique number generated would stay in RAM forever, eventually causing an Out-Of-Memory crash.

Scalability: The server would handle fewer concurrent users over time as the internal integer cache grew and consumed available system resources.

Performance: Python's internal lookup tables for these integers would grow massive. Searching the cache to see if a number already exists would become slower than just creating a new object.


## Exercise 6 (Challenge)

A student says:

"Since 5 is 5 is True, I should always use is instead of == for numbers because it is faster."

Write a response correcting this misunderstanding.

Explain:

what is actually checks,
why the behavior with small integers is an implementation optimization,
why == is the correct operator when comparing values.


The Correction: Never use is to compare numbers. While it might look faster in quick tests with small numbers, it will introduce silent, unpredictable bugs into your code as soon as your numbers get larger or smaller than the cached range.

What is actually checks: The is operator checks identity (whether two variables point to the exact same memory address).

The Optimization Trap: The fact that 5 is 5 evaluates to True is an internal CPython optimization detail, not a rule of the Python language. It fails for numbers like 1000 is 1000 in many environments.Why == is correct: The == operator checks equality (whether the data values inside the objects are equal). 

When comparing numbers, you care about the numerical value, not where it is stored in your computer's RAM.