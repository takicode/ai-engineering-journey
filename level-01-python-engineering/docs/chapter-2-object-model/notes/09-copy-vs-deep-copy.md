# Lesson 9 — Copy vs Deep Copy
## The Big Question

Imagine you have a house.

House
 ├── Kitchen
 ├── Bedroom
 └── Bathroom

Now someone asks:

    "Can I have a copy of your house?"

What exactly do they mean?

There are two possibilities.

### Possibility 1

They make a new front door.

But behind that door...

it's still the same rooms.

    House A
    |
    Kitchen
    Bedroom
    Bathroom

    House B
    |
    Kitchen
    Bedroom
    Bathroom

The houses look separate.

But they're secretly sharing everything inside.

Modify the kitchen...

both houses change.

### Possibility 2

Instead...

they rebuild

    another kitchen
    another bedroom
    another bathroom

Now you truly have two independent houses.

    House A

    Kitchen A
    Bedroom A
    Bathroom A

    -------------------

    House B

    Kitchen B
    Bedroom B
    Bathroom B

Nothing is shared.

Modify one house...

the other doesn't care.

This is exactly the difference between

shallow copy

deep copy
## Why does this matter?

Suppose you're training an AI model.

You have

Dataset

Images
Labels
Metadata
Transforms

If you accidentally make a shallow copy...

changing labels in one dataset...

changes labels in the other dataset.

Suddenly your validation set has been modified.

Now your model appears more accurate than it really is.

This is an actual source of bugs in ML pipelines.

Before Python

Let's think about references.

Suppose we have

    numbers

    ↓

    [List]

    ↓

    1
    2
    3

You already know

the variable isn't the list.

It points to the list.

Now suppose

backup = numbers

Did Python create another list?

No.

    numbers ───┐
               │
               ▼
             [1,2,3]
               ▲
               │
    backup ────┘

One list.

Two names.

Reference count increased.

Nothing copied.

Good.

Now imagine you actually request a copy.

backup = numbers.copy()

What should happen?

First thought

Many beginners think

Python copies

1
2
3

into another list.

That's partially true.

But what if the list contains objects?

Suppose

    [
        Dog(),
        Cat(),
        Bird()
    ]

Should Python

duplicate

every animal?

Or only duplicate

the list?

Those are VERY different operations.

The Real Question

When copying something...

What exactly are we copying?

The container?

Or everything inside the container?

This single question defines

shallow copy
deep copy

Let's Build Intuition

Imagine a bookshelf.

Bookshelf

↓

Book A

Book B

Book C

Now copy the bookshelf.

### Option A

Build another shelf.

Move nothing.

Just put labels pointing to the same books.

    Shelf A

    ↓

    Book A
    Book B
    Book C

    ----------------

    Shelf B

    ↓

    Book A
    Book B
    Book C

The shelves are different.

The books are shared.

### Option B

Build another shelf.

Then photocopy

every book.

    Shelf A

    ↓

    Book A
    Book B
    Book C

    ----------------

    Shelf B

    ↓

    Book A'
    Book B'
    Book C'

Nothing shared.

Everything independent.

That's

Shallow Copy

vs

Deep Copy.

### Python Terminology

Shallow Copy

Creates

a new container

but

does NOT create copies of the objects inside.

It copies the references.

    New List

    ↓

    same object

    same object

    same object

Deep Copy Creates a new container

AND

creates copies of everything inside.

    New List

    ↓

    new object

    new object

    new object
## Why Doesn't Python Always Deep Copy?

Excellent engineering question.

Imagine

Huge AI Model

↓

80 GB

If

copy(model)

duplicated everything...

Congratulations.

You just allocated another

80 GB.

Maybe

160 GB.

Maybe

320 GB.

Your computer dies.

Deep copying is expensive.

Very expensive.

Sometimes impossibly expensive.

So Python chooses the cheaper default.

## Mental Model

Never memorize

shallow vs deep copy.

Instead remember this:

Shallow Copy

Copies the house.

Shares the furniture.

---------------------

Deep Copy

Copies the house.

Copies the furniture.

If you remember that,

you'll almost never get confused.

One More Important Insight

This lesson is not really about copying.

It's about references.

Everything you've learned so far is leading to this realization:

    Objects

    ↓

    References

    ↓

    Mutability

    ↓

    Aliasing

    ↓

    Copying

Once you understand references deeply, copying becomes almost obvious.

