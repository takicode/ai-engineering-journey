## Lesson 2 — Local Scope

Why does Local Scope even exist?

Let's start with a question.

Imagine you write this:

def calculate_salary():
    tax = 200
    bonus = 500

Now imagine somewhere else in your program you write

print(tax)

Should this work?

Many beginners immediately think:

"Yes, because tax exists."

But here's the deeper question:

Exists where?

That single question leads us to one of Python's most important concepts.

Imagine an office building

Think of a company.

It has:

the CEO's office
HR
Finance
Engineering

Each department has its own filing cabinet.

Finance has

Tax Report
Payroll
Budget

Engineering has

Source Code
Models
API Keys

Suppose someone from HR walks into Engineering and says:

"Give me the Payroll spreadsheet."

Engineering replies:

"We don't have that."

Does the spreadsheet exist?

Yes.

Can Engineering see it?

No.

### Why?

Because it exists in a different department.

Python does exactly the same thing.

Every function gets its own "filing cabinet."

That filing cabinet is called its local namespace.

What happens when a function is called?

Suppose we have:

    def greet():
        name = "Taki"

The moment greet() is called, Python creates something new.

Not just a stack frame.

Inside that stack frame it also creates a namespace.

Conceptually:

Stack

    +---------------------------+
    | greet()                   |
    |                           |
    | Local Namespace           |
    |                           |
    | name ─────────► "Taki"    |
    +---------------------------+

Notice something important.

The variable isn't floating around the whole program.

It lives inside this function's namespace.

Another function
    def login():
        username = "Alice"

Now we call

greet()

login()

Conceptually:

Stack

    +----------------------+
    | login()              |
    | username -> "Alice"  |
    +----------------------+

    +----------------------+
    | greet()              |
    | name ----> "Taki"    |
    +----------------------+

Each function owns its own namespace.

They cannot accidentally see each other's variables.

Why is this important?

Imagine there were no local scope.

Every variable created anywhere would be dumped into one giant namespace.

    name
    username
    password
    tax
    bonus
    index
    result
    count
    count
    count
    count
    temp
    temp
    temp

What happens when two functions both use result

Which one wins?

Who overwrites whom?

You would constantly destroy other parts of your program without realizing it.

Local scope prevents this chaos.

## A real AI example

Imagine training a neural network.

One function computes the loss.

loss = ...

Another computes the gradients.

loss = ...

Another evaluates validation accuracy.

loss = ...

All three functions naturally want a variable called loss.

Because each function has its own local namespace, they can all use the same variable name safely.

Otherwise, one computation could overwrite another, producing incorrect results.

This isolation is one reason large machine learning codebases remain manageable.

## What actually lives in a local scope?

A local namespace typically contains:

Parameters
Variables created inside the function
Temporary intermediate values
References to objects

Notice the last point.

Just like everything we've learned:

The namespace stores names (references), not the objects themselves.

Local Namespace

x ─────────────► Integer Object (10)

numbers ───────► List Object

model ─────────► Neural Network Object

Nothing new here.

We're simply asking:

Where do these names live?

The answer is:

Inside the function's local namespace.

When does a local scope disappear?

Suppose:

    def greet():
        name = "Taki"

When the function finishes,

the stack frame is popped.

Since the namespace lives inside that stack frame,

the namespace disappears too.

    Call function
        ↓

    Create stack frame
        ↓

    Create local namespace
        ↓

    Run function
        ↓

    Return
        ↓

    Destroy stack frame
        ↓

    Destroy local namespace

The names disappear.

Whether the objects disappear depends on whether something else is still referencing them—exactly as you learned with reference counting and garbage collection.

## Mental Model

Think of a function call as renting a hotel room.

When you check in:

A room is prepared for you (stack frame).
Inside the room is your personal workspace (local namespace).
You put your belongings there (variable names).

When you check out:

The room is emptied.
Your workspace disappears.
Any belongings that nobody else owns are discarded.
Belongings that someone else still has (shared objects) continue to exist.

This ties together the ideas of stack frames, namespaces, references, and object lifetime into one coherent model.

