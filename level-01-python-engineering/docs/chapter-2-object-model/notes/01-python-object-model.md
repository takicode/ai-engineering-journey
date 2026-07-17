# Chapter 2 — Python's Object Model
# Lesson 1 — Variables Do Not Store Values

Read that sentence again.

Variables do not store values.

If you fully understand this lesson, then concepts like mutability, identity, copying, garbage collection, function arguments, and even parts of PyTorch become much easier.

A Question

Suppose you write:

x = 10

Almost everyone imagines this:

      +------+
      |  x   |
      +------+
      | 10   |
      +------+

That is not how Python thinks.

The Wrong Mental Model

Many languages teach:

      Variable
         │
      contains
         ▼
      Value

That model works well enough for beginners, but it isn't Python's model.

Python's Mental Model

Python thinks like this:

### Step 1

Create an object.

        +-----------+
        | Integer 10|
        +-----------+

Then:

### Step 2

Bind a name to it.

      x
      │
      ▼
      +-----------+
      | Integer 10|
      +-----------+

Notice something.

Where is the variable?

There isn't a "box" called x holding the number.

Instead:

an object exists in memory
x is simply a name that refers to that object

Python documentation actually talks about name binding, not "storing a value in a variable."

That wording is deliberate.

### Think Like Sticky Notes

Imagine your desk.

You have a book.

Book

Now put a sticky note on it.

Sticky Note: x

        x
        │
        ▼
      [Book]


The sticky note is not the book.

It simply tells you which book you're talking about.

Now add another sticky note.

         x
         \
          \
            ▼
         [Book]
            ▲
           /
          /
         y

Now both names refer to the same object.

This idea will become incredibly important later.

Another Example

         x = 10
         y = x

Most beginners imagine:

         x -> 10

         y -> 10

Or even:

         +----+    +----+
         |10  |    |10  |
         +----+    +----+

But conceptually, Python is closer to:

          +-----------+
          | Integer 10|
          +-----------+
             ▲     ▲
             │     │
             x     y

One object.

Two names.

### Why Does Python Work This Way?

Imagine a huge object.

      big_model = GPT_Model()

Suppose that model occupies 20 GB of memory.

Now imagine this:

another = big_model

If Python copied the whole object every time you assigned a variable...

      20 GB

      ↓

      20 GB

      ↓

      20 GB

      ↓

      20 GB

Your computer would run out of memory almost instantly.

Instead, Python simply creates another reference.

        big_model
            │
            ▼
      +------------------+
      | Huge AI Model    |
      +------------------+
            ▲
            │
         another

Almost free.

Very fast.

Very efficient.

Objects First, Names Second

This sentence is worth memorizing:

In Python, objects exist first. Names are bound to objects.

Not:

Variables contain values.

But:

Names refer to objects.

That distinction will explain almost every "weird" Python behavior you encounter later.

A Peek Under the Hood

When CPython executes:

x = 10

Conceptually, it does something like:

Create (or reuse) an integer object representing 10.
Store that object in memory.
Bind the name x to that object.

You don't need to worry yet about optimizations like integer caching—we'll come back to those later.

## Why This Matters for AI Engineering

Frameworks like NumPy and PyTorch rely heavily on object references.

When you write:

tensor2 = tensor1

Most people think they've made a copy.

Often, they haven't.

They've created another reference to the same underlying object.

Misunderstanding that can lead to subtle bugs, unexpected model behavior, and unnecessary memory usage.

### Key Ideas to Remember
Python variables are names, not storage boxes.
Objects live independently in memory.
Assignment binds a name to an object.
Multiple names can refer to the same object.
This design saves memory and improves performance.
Exercises

No coding yet. I want you to build the correct mental model first.



📚 Repository Work

After you complete these exercises:

Create docs/cheat-sheets/python-object-model.md.
Write your own one-page summary titled "Python Names, Objects, and References". Don't copy my wording; explain it in your own words. This will become one of your interview revision notes.

This chapter is one you'll revisit many times throughout your AI engineering journey.


