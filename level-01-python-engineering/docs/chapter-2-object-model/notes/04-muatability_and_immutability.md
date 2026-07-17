# Lesson 4 — Mutability vs Immutability

Consider this code.

    x = 10

    x = x + 1

Now compare it with this.

    numbers = [1, 2]

    numbers.append(3)

Both seem to "change something."

But something fundamentally different happened.

### Why?

That is today's lesson.

## What Does "Mutable" Mean?

Mutable means:

The object itself can be changed after it has been created.

Think about a whiteboard.

Write:

Hello

Later...

Erase it.

Write:

Python


It is still the same whiteboard.

Only the writing changed.

The object stayed the same.


## Immutable

Immutable means:

> **Once the object has been created, its contents can never change.**

Imagine carving words into stone.


HELLO


Can you erase it?

No.

If you want:


PYTHON


you carve an entirely new stone.

The old stone never changes.



# Python Immutable Types

The most common immutable objects are:


int

float

bool

str

tuple

frozenset

bytes


Once created...

they never change.


# Mutable Types

Common mutable objects include:


list

dict

set

bytearray

most class instances


These objects can change after creation.



# Let's Look at an Integer


    x = 10

Memory:

    x

    ↓

    +-----------+
    | Integer10 |
    +-----------+

Now:

    x = x + 1

What happens?

Many beginners think:

    Integer10

    ↓

    Integer11

Wrong.

Python cannot modify Integer10.

Instead...

Python computes:

10 + 1

Result:

11

Then creates another object.

    +-----------+
    | Integer10 |
    +-----------+

    +-----------+
    | Integer11 |
    +-----------+

Then moves the name.

    x

    ↓

    +-----------+
    | Integer11 |
    +-----------+

The Integer10 object never changed.

Now let Look at a List

numbers = [1, 2]

Memory:

numbers

↓

+----------------+
| [1,2]          |
+----------------+

Now:

numbers.append(3)

Did Python create another list?

No.

Instead...

The existing list changes.

Before

[1,2]

↓

After

[1,2,3]

Same object.

New contents.

The Biggest Difference

Immutable:

    Object

    ↓

    Cannot change

    ↓

    Need another object

Mutable:

    Object

    ↓

    Can change

    ↓

    Same object

## Why Have Mutable Objects?

Imagine editing a Word document.

Every time you typed one letter...

Imagine Word created an entirely new document.

    100 pages

    ↓

    type one letter

    ↓

    new 100-page document

Terrible.

Lists and dictionaries are mutable because changing them in place is efficient.

## Why Have Immutable Objects?

Now imagine passwords.

"OpenAI123"

If strings were mutable...

One part of your program could accidentally change:

OpenAI123

into

OpenAI124

while another part still expected the old value.

That would create chaos.

Immutability makes objects predictable.

Identity Changes?

Consider:

x = 10

x = x + 1

Identity before:

Object A

Identity after:

Object B

Different object.

Different identity.

Now compare:

    numbers = [1]

    numbers.append(2)

Identity before:

Object A

Identity after:

Object A

Same identity.

Only contents changed.

## Why This Matters in AI

Suppose:

weights = [...]

contains

100 million numbers

Training performs:

weights[i] = new_value

millions of times.

Imagine if every update created another list.

Training would take forever.

Instead...

Lists and tensors are mutable.

They update in place.

A Subtle Example

Consider:

a = [1,2]

b = a

Memory:

    a

    ↓

    +-------------+
    | [1,2]       |
    +-------------+
        ▲
        │
        b

Now:

a.append(3)

What happens?

Many beginners expect:

    a

    ↓

    [1,2,3]

    b

    ↓

    [1,2]

Wrong.

Both names point to the SAME object.

The object changed.

Memory:

    a

    ↓

    +---------------+
    | [1,2,3]       |
    +---------------+
        ▲
        │
        b

Both variables "changed."

Actually...

Neither variable changed.

The object changed.

This distinction is incredibly important.

Another Example

    a = "Python"

    b = a

Memory:

    a

    ↓

    "Python"

    ↑

    b

Now:

    a += "3"

Did the string change?

No.

Python creates:

"Python3"

Then rebinds:

a

Memory becomes:

a

↓

"Python3"



b

↓

"Python"

Again...

Strings are immutable.

Why Beginners Get Confused

They think:

    Variable

    ↓

    contains value

Reality:

    Name

    ↓

    Object

    ↓

    Mutable?

    ↓

    Can change

OR

Need another object

Everything depends on the object.

Not the variable.

## Mental Model

Instead of asking:

Did the variable change?

Ask:

Did the object change?

If yes...

it's mutable.

If no...

a new object was created.

Summary

Immutable objects:

cannot change
reassignment creates another object
examples:
int
float
bool
string
tuple

Mutable objects:

can change
identity stays the same
examples:
list
dictionary
set
One Important Note

There's a phrase you'll hear often:

"Everything in Python is an object."

That's true.

But not every object behaves the same way.

The first question an experienced Python developer asks about an object is:

Is it mutable or immutable?

That single question predicts a huge amount of Python's behavior.

Exercises

Take your time. These are some of the most important exercises we've done.


