# Lesson 5 — Python's Argument Passing Model

This is arguably the most misunderstood topic in Python.

Even experienced developers will confidently say things like:

"Python is pass-by-reference."

Others say:

"Python is pass-by-value."

Both are incomplete.

By the end of this lesson you'll understand exactly what Python does.

## The Debate

Across programming languages you'll hear terms like:

    Pass-by-Value
    Pass-by-Reference
    Pass-by-Pointer

People try to force Python into one of these categories.

But Python's execution model doesn't fit neatly into any of them.

Instead, Python uses what is commonly called:

    Pass-by-Object-Sharing

    or

    Pass-by-Assignment

These names describe Python's behavior much more accurately.

Let's Start with What Actually Happens

Suppose

    numbers = [1, 2, 3]

    process(numbers)

We already know:

Before the call

Global Namespace

    numbers
        │
        ▼
    [1,2,3]

The list already exists.

Now Python evaluates

    process(numbers)

### Step 1

It evaluates the expression

numbers

That expression produces

the existing list object

Not the variable.

The object.

### Step 2

Python creates an execution frame.

Execution Frame

### Step 3

The parameter becomes a local variable.

Suppose

    def process(data):

Now

    Local Namespace

    data

exists.

### Step 4

Python binds

data

to

the exact same list object.

Conceptually

Global Namespace

    numbers
        │
        │
        ▼
    [1,2,3]
        ▲
        │
        │
    Local Namespace

data

Nothing copied.

Nothing cloned.

Nothing moved.

### What Gets Passed?

This is the key question.

People often say

"Python passes variables."

No.

Variables never leave their namespace.

### The variable

numbers

stays exactly where it was.

Instead,

Python evaluates

numbers into the list object

and binds the parameter to that object.

### Why Lists Appear to be "Passed by Reference"

Suppose

    def process(data):
        data.append(4)

Both names point to

    [1,2,3]

When

    data.append(4)

executes,

the list object changes.

Not the variable.

The object.

So after the call

    numbers

        ↓

    [1,2,3,4]

appears changed.

Because it is looking at the same object.

But Now Watch This

Suppose

    def process(data):
        data = [10, 20]

Many beginners expect

numbers

to become

[10,20]

It doesn't.

Why?

Because this is rebinding.

Remember Chapter 2.

The assignment operator changes names.

Not objects.

So

instead of

    numbers

       ↓

    [1,2,3]

becoming

    numbers

       ↓

    [10,20]

Python creates

New List

    [10,20]

and changes only

data

to point there.

Now we have

    numbers
        │
        ▼
    [1,2,3]

      data
        │
        ▼
    [10,20]

The original object never changed.

Only the local name changed.

## Mutation vs Rebinding

This is the heart of Python's calling model.

Mutation
    data.append(4)

Changes

the object.

Everyone sees it.

Rebinding
    data = [10,20]

Changes

the local variable.

Nobody else sees it.

Everything you've learned since Chapter 2 leads to this distinction.

## Why People Get Confused

Because these two pieces of code behave differently.

Example A

    def process(data):
        data.append(4)

Caller changes.

Example B

    def process(data):
        data = []

Caller doesn't change.

People think

"Python changed its passing mechanism."

It didn't.

The passing mechanism is identical.

Only the operation performed afterward is different.

## The Actual Rule

Python always does exactly the same thing.

    Evaluate the argument.
    Obtain the object.
    Create a local variable.
    Bind that local variable to the same object.

Everything after that depends on whether you:

    mutate the object

    or

    rebind the local name.
## Why Python Uses This Model

Imagine calling

train(model)

where

model = 60 GB

If Python copied the model...

Every function call would require

another

60 GB.

Impossible.

Instead

Global

      model
        │
        ▼
    60 GB Model
        ▲
        │
    train()

parameter

Two names.

One model.

## Why AI Depends on This

Libraries like

NumPy
PyTorch
TensorFlow
JAX

constantly pass around

tensors
datasets
neural networks
gradients
optimizer state

Some of these occupy

gigabytes of RAM

or

gigabytes of GPU memory.

Passing references to existing objects makes function calls effectively constant-time with respect to object size. The cost of the call doesn't grow because the object is larger; the function simply gets another name bound to the same object.

## The Mental Model

Never think

Python copied the object.

Instead think

    Caller

      ↓

    Object

      ↓

    Function receives another name

       ↓

    Same object

That's the entire model.

### The Complete Timeline

Caller Namespace

    numbers
        │
        ▼
    [1,2,3]

    ↓

    Call

    ↓

    Execution Frame

    ↓

    Create local variable

    ↓

    data
        │
        ▼
    [1,2,3]

    ↓

    Either

    Mutate Object

    or

    Rebind Local Name

Everything you've learned about

Names
Objects
References
Namespaces
Frames
Scope
Parameters
Arguments

comes together here.

One Important Terminology Note

You'll still hear experienced developers say:

"Python passes references."

In practice, most people understand what they mean.

However, the more precise description is:

Python passes object references by assignment (pass-by-object-sharing).

This wording emphasizes that the function receives another binding to the same object—not a special "reference variable" in the C++ sense.

