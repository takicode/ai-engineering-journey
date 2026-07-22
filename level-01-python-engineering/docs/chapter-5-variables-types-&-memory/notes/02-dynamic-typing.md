# Lesson 2 — Dynamic Typing

This is one of the biggest misconceptions in Python.

People say:

"Python variables have no types."

Others say:

"Everything has a type."

They sound contradictory.

Both are true.

The trick is understanding what has the type.

Let's start with code

    x = 10

    print(type(x))

    Output:

    <class 'int'>

Now:

    x = "hello"

    print(type(x))

    Output:

    <class 'str'>

Now:

    x = [1, 2, 3]

    print(type(x))

    Output:

    <class 'list'>

Same variable.

Three different types.

The obvious question

How can one variable be

an integer,
then a string,
then a list?

Wouldn't that violate everything we've learned?

No.

Because the variable never had a type.

What actually changed?

Let's walk through it.

Initially:

    x = 10

Memory:

Global Namespace

    x ───────────────► int object (10)

The name x points to an integer object.

Notice something.

The integer has the type.

Not x.

Next line:

    x = "hello"

Python does not transform the integer into a string.

Instead:

Before

    x ─────────► int(10)

After:

    x ─────────► str("hello")

int(10)

The integer object is untouched.

The string object already exists (or is created).

Python simply changes where x points.

This is called rebinding.

We've actually studied rebinding before in Chapter 2.

Dynamic typing is one of its biggest consequences.

Then:

    x = [1, 2, 3]

Now:

    x ─────────► list([1,2,3])

    str("hello")

    int(10)

Again

nothing about the previous objects changes.

Only the reference changes.

Dynamic typing in one sentence

Python is dynamically typed because

names are untyped; objects carry their own types.

Not:

variables change type.

Instead:

variables change which object they reference.

That is a much more accurate statement.

Compare with Go (which you already know)

In Go:

    x := 10

    x = "hello" // ERROR

Why?

Because in Go:

x itself has type int.

The variable owns the type.

Python:

    x = 10

    x = "hello"

    x = [1, 2, 3]

Perfectly legal.

Why?

Because x owns nothing except a reference.

The objects own their types.

Let's trace code

Example:

    x = 5

    y = x

    x = "AI"

Step 1

    x ─────► int(5)

Step 2

    x ─────► int(5)
            ▲
            │
    y ─────────┘

Two names.

One object.

Step 3

    x ─────► str("AI")

    y ─────► int(5)

Did the integer become a string?

No.

Did y change?

No.

Why?

Because assignment changes names—not objects.

Let's make it more interesting
    numbers = [1, 2]

    alias = numbers

    numbers = [10, 20]

Think before reading.

After the last line:

Does alias point to

[1,2]

or

[10,20]

Answer:

    numbers ───► [10,20]

    alias ─────► [1,2]

Why?

Because assignment never edits an object.

It rebinds a name.

## AI Engineering Example

Imagine:

    model = load_model()

    backup = model

Memory:

    model ─────► Neural Network

    backup ────▲

Now:

    model = load_new_model()

Memory:

    model ─────► New Neural Network

    backup ───► Old Neural Network

The original model wasn't modified.

The name model simply changed what it referenced.

This distinction is critical in production systems where multiple components may still hold references to the original model.

## Why Dynamic Typing Exists

Python values flexibility.

Imagine an interactive notebook:

    data = load_csv()

Later:

    data = preprocess(data)

Later:

    data = convert_to_tensor(data)

Later:

    data = model(data)

data now refers to:

    a DataFrame
    a processed DataFrame
    a Tensor
    model output

One descriptive name can follow the logical "thing" you're working with, even though the underlying object type changes over time.

## Best Practice

Just because Python allows this:

    x = 10
    x = "AI"
    x = [1, 2]
    x = lambda a: a * 2

doesn't mean it's good code.

Good engineers choose meaningful names:

    count = 10

    message = "AI"

    numbers = [1, 2]

    double = lambda a: a * 2

Dynamic typing provides flexibility; good naming provides readability.

## Mental Model

Never think:

Variable changes type.

Instead think:

The name changes which object it references.

The object owns the type.

The name owns nothing except a reference.

