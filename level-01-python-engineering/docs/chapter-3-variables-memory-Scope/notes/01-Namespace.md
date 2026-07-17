# Lesson 1 — What is a Namespace?

The question

Imagine you write

x = 10

We already know:

An integer object exists.

The name x points to it.

But here's the question nobody asks:

Where is the name x stored?

Not the object.

The name.

Where does Python keep it?

Many beginners imagine something like this:

RAM

+----------------------+

x

↓

10

+----------------------+

That's not how Python thinks.

Let's make it harder.

Imagine you write:

x = 10
y = [1,2,3]
name = "Taki"

Question:

Where are these names?

x
y
name

Are they floating around in RAM?

How does Python find them?

Imagine a giant office

Suppose a company has

100,000 employees

Every employee has

a name
a desk

If someone says

"Go find Sarah."

Would you walk through every office looking for Sarah?

Of course not.

The company has a directory.

Sarah  → Desk 42

John   → Desk 81

Alice  → Desk 19

You look in the directory.

Then you go directly to the desk.

Python does exactly the same thing.

Python keeps a dictionary

This is the first big idea.

Python stores names inside a special dictionary.

Conceptually,

Namespace

----------------------------

"x" ---------> Object A

"y" ---------> Object B

"name" ------> Object C

----------------------------

Notice something.

The namespace does not contain

integers
lists
strings

It contains

    name

      ↓

    reference

That's all.

The objects still live on the heap.

Namespace

    "x" ------------+

                    |

                    ▼

            Integer 10



"y" ------------+

                |

                ▼

          List Object

Why is this brilliant?

Imagine Python had

10 million variables.

If Python searched memory every time you typed

print(score)

your computer would crawl.

Instead it asks

Namespace:

Do you have a name called

"score"?

Dictionary lookup.

Milliseconds.

This explains something interesting

Suppose

x = 10

y = x

People often imagine

    x

    ↓

    10

    y

    ↓

    10

That's close.

But we're missing one layer.

Actually

Namespace

    "x" ----------+

                |

    "y" ----------+

                |

                ▼

            Integer 10

The namespace stores

"x"

"y"

The heap stores

Integer 10

Even functions work this way

    def greet():
        ...

creates

Namespace

    "greet"

       ↓

    Function Object

Classes

Namespace

    "Person"

    ↓

    Class Object

Modules

Namespace

    "math"

    ↓

    Module Object

Everything you've learned still applies.

The only new discovery is

Names themselves live inside a namespace.

A namespace is basically a dictionary

Not exactly a Python dict in every implementation, but conceptually that's the right mental model.

    {

    "x": reference,

    "y": reference,

    "name": reference,

    "greet": reference

    }

Why this matters

Everything in Python starts making sense once you realize:

Python does not search memory for variable names.

It asks:

Which namespace am I currently using?

Then it performs a dictionary lookup.

That one idea explains:

local variables
global variables
functions
modules
classes
imports
closures
the LEGB rule

Nearly all of Chapter 3 grows naturally from this concept.

## Mental Model

From now on, visualize Python like this:

              Namespace
        +---------------------+
        | "x"     → ref ------+------------------+
        | "y"     → ref --+   |                  |
        | "name"  → ref   |   |                  |
        +-----------------|---+                  |
                          |                      |
                          ▼                      ▼
                     Integer 10          String "Taki"
                           (Heap Objects)

Notice that:

Names live in the namespace.
Objects live on the heap.
References connect the two.

That is the complete picture you've been building toward since Chapter 2.


