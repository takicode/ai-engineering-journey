# Lesson 3 — Assignment & Rebinding

When Python executes:

x = 10

what actually happens?

Many beginners imagine this:

    Variable x
    +------+
    |  10  |
    +------+

That picture is wrong.

Python variables are not boxes.

We've already established that.

Instead:

    Name x
    │
    ▼
    +------------+
    | Integer 10 |
    +------------+

The name points to an object.

Now Let's Reassign
x = 10

x = 20

Many people think Python does this:

Before

    x
    │
    ▼
    +------------+
    | Integer 10 |
    +------------+

    ↓

    Change object

    x
    │
    ▼
    +------------+
    | Integer 20 |
    +------------+

That is NOT what happens.

Python integers are immutable.

The object cannot change.

Instead:

Step 1

    x
    │
    ▼
    +------------+
    | Integer 10 |
    +------------+

Then:

x = 20

    Python creates another object.

    +------------+      +------------+
    | Integer 10 |      | Integer 20 |
    +------------+      +------------+

    Then moves the name.

            x
            │
            ▼
    +------------+      +------------+
    | Integer 10 |      | Integer 20 |
    +------------+      +------------+

The old object stays exactly as it was.

The name moved.

### This Is Called Rebinding

Python doesn't modify the object.

It rebinds the name.

Think of a sticky note.

Sticky note:

x

You stick it on

Object A

Later you peel it off

and stick it onto

Object B

Did either object change?

No.

Only the label moved.

Another Example

        x = 10
        y = x

Memory:

        x
        │
        ▼
    +--------+
    |   10   |
    +--------+
        ▲
        │
        y

Now:

x = 20

Python does not change 10.

Instead:

        y
        │
        ▼
    +--------+
    |   10   |
    +--------+

        x
        │
        ▼
    +--------+
    |   20   |
    +--------+

Now ask yourself:

Why is y still 10?

Because nothing ever changed the original object.

Only x moved.

Why Doesn't Python Modify 10?

### Because integers are immutable.

The integer object literally represents:

10

Changing it into

20

would mean changing reality for every name pointing there.

Imagine:

        a = 10
        b = 10
        c = 10

If Python modified the object itself:

a = 20

suddenly

b

c

would also become 20.

That would be a disaster.

So Python simply creates another integer object.

Assignment Does One Thing

This is worth memorizing.

### Assignment does not change objects.

### Assignment binds a name to an object.

Or, if the name already exists:

Assignment rebinds the name.

That single sentence explains a huge amount of Python behavior.

A More Interesting Example

    a = 100

    b = a

    c = b

How many integer objects exist?

Answer:

One.

        a
        │
        ▼
     +------+
     | 100  |
     +------+
        ▲
        │
        b
        ▲
        │
        c

Three names.

One object.

Then:

b = 200

Now:

        a
        │
        ▼
     +------+
     | 100  |
     +------+
        ▲
        │
        c


        b
        │
        ▼
     +------+
     | 200  |
     +------+

Again—

No object changed.

Only one label moved.

## Why This Matters for AI

Imagine:

model = huge_neural_network

The model occupies:

18 GB

Now:

backup = model

Did Python copy 18 GB?

No.

It simply created another reference.

            model  ───────┐
                          │
            backup ───────┘

                Huge Neural Network
                        18 GB`

Instant.

No memory wasted.

If assignment copied objects automatically:

backup = model

would allocate another

18 GB

which would make AI nearly impossible on ordinary hardware.

## Mental Model

Never think:

Variable contains value.

Instead think:

Name points to object.

And never think:

Assignment changes the value.

Instead think:

Assignment moves the name to another object.

Common Beginner Mistake

Someone writes:

x = 10

y = x

x = 20

Then says:

Python changed x.

That's not quite right.

A more accurate statement is:

Python rebound the name x to a different integer object.

That wording reflects what actually happened in memory.




