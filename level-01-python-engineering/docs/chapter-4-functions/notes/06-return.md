# Lesson 6 — Return Values

Most people think of return as:

"Send a value back."

That explanation is correct...

...but it's incomplete.

Just as we asked what really happens when passing an argument, we're now going to ask:

What actually happens when Python returns an object?

This lesson will complete your mental model of function calls.

Start with a Simple Function

    def create():
        return [1, 2, 3]

Suppose we later write:

    numbers = create()

Many beginners imagine something like this:

      Function

         ↓

    creates list

         ↓

    copies list

         ↓

    caller receives copy

That is not what happens.

## What Actually Happens?

Let's follow the timeline.

### Step 1 — Function Call

Python finds the existing function object.

      create
        │
        ▼
    Function Object
### Step 2 — Create Execution Frame

A brand-new execution frame is created.

Execution Frame

Exactly as we've already learned.

### Step 3 — Create the List

The function executes

return [1, 2, 3]

This creates

Heap

[1,2,3]

A normal list object.

Nothing special because it will be returned.

## Step 4 — Evaluate the Return Expression

Notice something important.

Python does not return syntax.

It returns the result of evaluating an expression.

For example

    return x

means

Evaluate

x

to obtain an object.

Likewise

    return x + y

means

Evaluate

x + y

first.

Then return the resulting object.

## What Gets Returned?

Exactly like arguments...

Python returns

the object.

Not the variable.

Suppose

    def create():

        numbers = [1,2,3]

        return numbers

Notice something interesting.

Python does not return

numbers

The variable never leaves the function.

Instead

Python evaluates

numbers

to obtain

the list object

Then returns that object.

Exactly the same idea we learned with arguments.

## What Happens Next?

Suppose

result = create()

Python receives

the returned object.

Then

Global Namespace

result

is bound to

that same object.

Conceptually

Execution Frame

   numbers
      │
      ▼
   [1,2,3]

      ↓

    Return

      ↓

Global Namespace

   result
      │
      ▼
   [1,2,3]

Notice what changed.

The object stayed exactly where it was.

Only another name became bound to it.

Then the Frame Disappears

Immediately after returning,

the execution frame is destroyed.

That means

numbers

disappears.

But

result

still points to

the list.

So the object survives.

Exactly like Chapter 3.

Return Does Not Copy Objects

Suppose

    model = load_model()

returns

a

45 GB neural network

Python does not

copy

45 GB.

Instead

Function Frame

    model
      │
      ▼
    45 GB Model

      ↓

    return

      ↓

    Caller

    trained_model
        │
        ▼
    45 GB Model

The execution frame disappears.

The caller now owns the reference.

One object.

Different name.

Returning Mutable Objects

Suppose

    def create():

        data = []

        return data

After the function returns,

the caller receives

the exact same list object.

If the caller later does

numbers.append(10)

the returned list changes.

Nothing mysterious happened.

The caller owns the only remaining reference.

Returning Immutable Objects

Suppose

    def create():
        return 100

Same idea.

Python returns

the integer object.

The caller binds a name to it.

There is no special rule for immutable objects.

The mechanism is identical.

Only later behavior differs because integers cannot be mutated.

Return is the Mirror of Arguments

Look carefully.

Argument Passing

    Caller

      ↓

    Object

      ↓

    Function Parameter

Return Values

    Function

       ↓

    Object

       ↓

    Caller Variable

They're mirror images.

Complete Timeline

Suppose

    def square(x):
        return x * x

result = square(5)

Conceptually

    Caller

       ↓

    Evaluate argument

        ↓

    Obtain object

        ↓

    Create execution frame

        ↓

    Bind parameter

        ↓

    Execute body

        ↓

    Evaluate return expression

        ↓

    Obtain result object

        ↓

    Destroy execution frame

        ↓

    Bind caller variable

        ↓

    Continue execution

Notice

Objects never travel.

Names never travel.

Execution frames never travel.

Only bindings change.

## Why This Matters for AI

Imagine

    embeddings = generate_embeddings(...)

The embedding matrix may occupy

several gigabytes.

Python doesn't copy it when returning.

Otherwise

every preprocessing stage

every inference stage

every training stage

would constantly duplicate huge tensors.

Instead

Python simply returns

the existing object.

The caller becomes its new owner.

This is why chaining together computational pipelines remains efficient even when dealing with large in-memory objects.

## The Mental Model

Never think

"The function sends a variable back."

Instead think

    Function evaluates an expression

    ↓

    Obtains an object

    ↓

    Caller binds a name

    ↓

    Function frame disappears

Everything we've learned about

objects
names
references
namespaces
frames
lifetime

still applies.

Nothing new was invented for return.

