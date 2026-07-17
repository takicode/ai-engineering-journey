# Exercises

As always, don't run the code. Reason from the mental model we've built.

## Exercise 1

In your own words:

What does the statement "Everything is an object" actually mean?

Do not simply list examples.

Explain the underlying idea.

The phrase means that Python applies a single, universal blueprint to all data structures in memory. Every piece of data—no matter how simple or complex—carries an identity (a unique memory address), a type (telling Python what it is), and value data. 

In many languages, numbers are raw data while functions are just instructions. In Python, a function or a class is treated exactly like an integer: a physical entity that sits in a memory block, can be moved around, and can be inspected at runtime.

## Exercise 2

Suppose you write:

def greet():
    print("Hello")

a = greet
b = greet

Conceptually draw the memory using ASCII.

Answer:

How many function objects exist?
How many names exist?
What is the conceptual reference count of the function object (ignoring Python's internal references)?

    Names (Variables)        Memory Object
    +-------+                +-------------------------+

    | greet | ----+--------> |     Function Object     |
    +-------+     |          |  Code: print("Hello")   |
    +-------+     |          |                         |

    |   a   | ----+          |  Ref Count: 3           |
    +-------+     |          +-------------------------+
    +-------+     |

    |   b   | ----+
    +-------+

How many function objects exist? Exactly 1 function object.

How many names exist? There are 3 names (greet, a, and b).

What is the conceptual reference count? 3 (excluding Python's internal tracker).

## Exercise 3

Suppose:

class Person:
    pass

A = Person
B = Person

Answer conceptually:

How many class objects exist?
What do A and B point to?
Was the class copied?

Explain your reasoning.

How many class objects exist? Exactly 1.

What do A and B point to? Both names point to that single, shared Person class object in memory.

Was the class copied? No. Assigning a class to a new variable name merely creates a new pointer to the existing class blueprint. It does not duplicate the class architecture.

## Exercise 4

Why is treating functions as objects one of Python's greatest strengths?

Think about:

callbacks
decorators
AI libraries
flexibility
code reuse

Callbacks & AI Libraries: You can pass a function directly into another function as an argument. In machine learning libraries, you can pass a specific mathematical loss function or activation function straight into a model's configuration block.

Decorators: Because functions are objects, you can wrap them inside other functions to add features (like logging, authentication, or timing) without rewriting the core code.

Flexibility & Reuse: Functions can be stored inside lists or dictionaries. This lets you map user input strings directly to executable function objects, creating clean, scalable routing systems.


## Exercise 5 (Thinking)

Imagine Python did not treat functions as objects.

Name at least four powerful Python features that would become impossible or much harder to implement.

Think beyond syntax—consider how modern frameworks and libraries are designed.

Decorators (@app.route / @property): Web frameworks like FastAPI or Flask would lose their clean routing syntax because you couldn't pass a route function into a configuration wrapper.

Functional Programming Tools (map, filter, any): You would not be able to pass filtering logic or transformation formulas directly into collections.

Event Handlers: Graphical interfaces (GUIs) and asynchronous web scrapers would require complex, boilerplate structural objects just to tell a button what task to execute when clicked.

Dynamic Routing Tables: Storing tasks inside dictionaries or queues (like background worker systems like Celery) would fail, as you couldn't pass executable function payloads over structural systems.

## Exercise 6 (Challenge)

A student says:

"Only variables are objects. Functions and classes are different."

Write a response correcting this misunderstanding.

Explain:

what a variable actually is,
what an object actually is,
why numbers, functions, classes, and even modules all fit into the same object model.


The Correction: Variables are actually never objects. A variable is simply a string name attached to a sticky note that points to an object in memory.

What an Object is: An object is the actual block of data living at a memory address.

Why everything fits the model: In Python, a number like 5, a function like greet, a class like Person, and even an imported module are all packaged exactly the same way. They all live in memory blocks, possess an internal __dict__ or type system, can have attributes attached to them, and can be safely passed across your program as data payloads.