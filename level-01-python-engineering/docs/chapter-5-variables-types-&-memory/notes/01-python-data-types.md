# Lesson 1 — Python Data Types

Most tutorials begin like this:

Python has integers, floats, strings, lists, tuples...

That's a list to memorize.

We're going to answer a much deeper question.

### The Real Question

What is a type?

Not:

What types exist?

but

What does "type" actually mean inside Python?

Let's start from what we already know

From Chapter 2, we established:

Everything in Python is an object.
Objects live on the heap.
Names point to objects.
Functions are objects.
Classes are objects.

So here's an interesting question.

If everything is an object...

what makes one object behave differently from another?

Why can one object be added?

    5 + 3

while another can be indexed?

    numbers[0]

Why can another be called?

    train()

Why can another be iterated?

    for x in items:

Same language.

Same heap.

Same objects.

Different behavior.

Where does that behavior come from?

## The Blueprint Idea

Imagine a car factory.

You don't build every car from scratch by making up the rules each time.

Instead you have a blueprint.

The blueprint specifies:

number of wheels
engine placement
doors
steering
dimensions

Every car produced from that blueprint follows those rules.

Python objects work similarly.

Every object is created from a type.

The type defines:

    what operations are allowed
    what data the object stores
    how it behaves
    what methods it has

For example,

    5

is an object.

Its type tells Python:

addition is allowed
subtraction is allowed
multiplication is allowed
division is allowed

A list object's type tells Python:

indexing is allowed
append exists
pop exists
extend exists

A function object's type tells Python:

    calling with ()
    parameters
    return values
    closures
    defaults

Notice something important.

The behavior is not stored in the variable.

It isn't even stored separately for every object.

The behavior comes from the object's type.

## A Type Is a Specification

Think of a type as answering three questions:

1. What data does this object contain?


Example:

An integer stores a numeric value.

A list stores references to other objects.

A function stores bytecode, defaults, globals, and metadata.

2. What operations are valid?

For example,

An integer supports:

+
-
*
/

A string supports:

+
[]
in

A function supports:

()

Different operations.

Different behavior.

3. How should Python perform those operations?

When Python evaluates:

5 + 2

it doesn't magically know how to add.

Instead, it asks the integer type:

"How do I perform addition for two integer objects?"

Likewise,

"AI" + " Engineering"

uses the string type's implementation of +, which means concatenation, not arithmetic.

The same operator (+) has different meanings because the type defines its behavior.

## Type vs Object

This is one of the biggest conceptual distinctions in Python.

An object is an individual thing.

A type is the specification that describes how objects of that kind behave.

For example:

    42

is an object.

    43

is another object.

They are different objects.

But they share the same type.

Likewise,

    "hello"

    and

    "world"

are different objects.

Same type.

Different data.

## Why This Design Matters

Imagine if every integer object stored its own copy of:

    how to add
    how to subtract
    how to multiply
    how to compare
    how to print itself

Every integer would carry identical behavior.

That would waste enormous amounts of memory.

Instead, Python stores the behavior once in the type, and every object of that type uses it.

This makes Python both more memory-efficient and more consistent.

## AI Engineering Connection

This idea appears everywhere in AI.

Consider a PyTorch tensor.

Each tensor object contains its own data (its numerical values), but it doesn't reinvent how matrix multiplication, slicing, reshaping, or moving to a GPU works.

Instead, all tensor objects share the behavior defined by the tensor type.

The same is true for NumPy arrays, Pandas DataFrames, and many other Python objects you'll use in AI. Understanding that behavior comes from the type—not from each individual object—is a key mental model for working effectively with these libraries.

## Mental Model

Think of Python like this:

                Object
          +------------------+
          |      Data        |
          |                  |
          +------------------+
                   |
                   v
              Has a Type
                   |
                   v
         +----------------------+
         | Defines Behavior     |
         | Defines Operations   |
         | Defines Structure    |
         +----------------------+

An object is the instance.

The type is the definition.

The object holds the data.

The type tells Python what that object can do.

