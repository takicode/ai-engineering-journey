# Lesson 10 — Everything is an Object
The Big Question

Let's begin with something you've seen thousands of times.

    x = 10

Question:

What is 10?

You now know the answer.

It is an integer object.

Not surprising anymore.

Now let's look at this.

    message = "Hello"

What is "Hello"?

A string object.

Still easy.

Now this.

    numbers = [1, 2, 3]

What is the list?

A list object.

Good.

Now this.

        def greet():
            print("Hello")

Question:

What is greet?

Most beginners answer:

A function.

That's true…

…but incomplete.

The better answer is:

A function object.

Now this.

    class Person:
        pass

What is Person?

Most people say:

A class.

Again…

that's incomplete.

The better answer is:

A class object.

Already something interesting is happening.

Python treats

numbers
strings
lists
functions
classes

all the same way.

They're all objects.

## What Is an Object?

Let's build intuition.

Imagine a city.

Every building has

an address
a purpose
information about itself

A hospital

has an address
knows it's a hospital
contains equipment

A school

has an address
knows it's a school
contains classrooms

A library

has an address
knows it's a library
contains books

Different contents.

Same basic structure.

Objects are similar.

Every Python object has

an identity (where it lives)
a type (what it is)
a value (its data)

Conceptually:

    Object

    ├── Identity
    ├── Type
    └── Value

We've actually been studying this for the entire chapter.

## The Secret

When Python creates anything...

it wraps it inside an object.

Not just numbers.

Everything.

Consider:

    42

Conceptually:

    Integer Object

    Type:
        int

    Value:
        42

    Identity:
        0x...

Now:

    "OpenAI"

Conceptually:

    String Object

    Type:
        str

    Value:
        "OpenAI"

    Identity:
        0x...

Now:

    [1, 2, 3]

Conceptually:

    List Object

    Type:
        list

    Identity:
        0x...

    Contains

    ↓

    references

Now something surprising.

    def add(a, b):
        return a + b

Conceptually:

    Function Object

    Name:
        add

    Parameters:
        a
        b

    Code:
        ...

    Identity:
        0x...

A function is literally an object living in memory.

## Why Does This Matter?

Because objects can be referenced.

Remember this?

    x = 10

The name points to an object.

Exactly the same thing happens here.

    f = add

People often think

"I'm copying the function."

No.

You're copying a reference to a function object.

Exactly like:

x = y

Memory:

    add ──────┐
              │
              ▼
        Function Object
              ▲
              │
    f─────────┘

One function.

Two names.

Reference count increases.

Sound familiar?

It should.

It's the exact same model we've used all chapter.

Functions Behave Like Objects

Because they are objects.

You can:

Store them.

operations = [add, subtract]

Pass them.

process(add)

Return them.

return add

Assign them.

f = add

This isn't a special feature.

It's a consequence of:

Functions are objects.

Classes Are Objects Too

This surprises many developers.

    class Dog:
        pass

Dog isn't just a blueprint.

Dog itself is an object.

It has

an identity
a type
attributes

Conceptually:

    Dog

    ↓

    Class Object

Then:

    dog = Dog()

creates

    Dog

    ↓

    Class Object

    ↓

    creates

    ↓

    Dog Instance Object

Notice:

Objects create other objects.

Why Python Chose This Design

Imagine if functions weren't objects.

You couldn't do this:

    sort(data, key=len)

because len couldn't be passed around.

Imagine if classes weren't objects.

Frameworks like Django or FastAPI couldn't inspect them.

Decorators wouldn't exist.

Many AI libraries would become awkward or impossible to design elegantly.

Python's flexibility comes from treating everything uniformly.

## AI Engineering Connection

Consider:

model = NeuralNetwork()

model points to an object.

Now:

optimizer(model)

You're passing a reference to that model object.

Now:

train(model)

Still the same object.

No 10 GB copy of the neural network was made.

Exactly the same reference model you've learned all chapter.

Understanding this explains why Python can manipulate very large models efficiently.

Everything We've Learned Comes Together

Let's connect the dots.

    Object Created

    ↓

    Reference

    ↓

    Identity

    ↓

    Reference Count

    ↓

    Garbage Collection

    ↓

    Mutability

    ↓

    Copying

    ↓

    Everything is an Object

This final lesson isn't introducing a new idea.

It's revealing that every previous lesson applies to almost everything in Python.

## Mental Model

If you remember only one diagram from this lesson, make it this one:

                Objects

        Number
        String
        List
        Dictionary
        Function
        Class
        Module
        File
        AI Model

              │

        All have

        Identity
        Type
        Value

        All use references

        All participate in
        Python's memory model

That's the Python object model in one picture.

