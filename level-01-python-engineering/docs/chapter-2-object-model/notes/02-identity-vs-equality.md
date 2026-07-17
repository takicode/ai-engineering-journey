## Lesson 2 — Identity vs Equality (is vs ==)

Suppose I show you these two phones.

📱 Phone A

📱 Phone B

Question 1:

Are they the same kind of phone?

Maybe yes.

Question 2:

Are they literally the same physical phone?

Maybe not.

Those are two completely different questions.

Python has two completely different operators for asking them.

## Equality (==)

Equality asks:

Do these two objects represent the same value?

Example:

5 == 5

Answer:

True

Easy.

Now:

"AI" == "AI"

Again:

True

Because the values are equal.

Notice something.

Python doesn't care where those objects live.

It only cares about the value they represent.

Think of it like this:

Book A

Title:
Python

Book B

Title:
Python

Different books.

Same title.

Equality says:

These represent the same information.

## Identity (is)

Identity asks a completely different question.

Instead of asking:

Do they have the same value?

It asks:

Are these literally the exact same object in memory?

Think back to yesterday.

We learned:

Names point to objects.

Identity asks whether two names point to the same object.

Example

Imagine this.

          +----------------+
          | Integer Object |
          |      10        |
          +----------------+
              ▲        ▲
              │        │
              x        y

Now ask:

x is y

Python answers:

True

because:

Both names point to the exact same object.

Another Example

Imagine instead:

        x                 y
        │                 │
        ▼                 ▼

+-----------+      +-----------+
| Integer 10|      | Integer 10|
+-----------+      +-----------+

Now:

x == y

Answer:

True

because:

The values are equal.

But:

x is y

Answer:

False

because:

Different objects.

Another Analogy

Imagine twins.

Twin A

Twin B

Ask:

Are they equal?

In many ways:

same height
same face
same DNA

Maybe yes.

Ask:

Are they literally the same human?

No.

That's identity.

Why Python Needs Both

Imagine a dictionary.

        user = {
            "name": "Taki"
        }

Later:

        another = user

Conceptually:

        another
            │
            ▼
        +----------------+
        | Dictionary     |
        | name = Taki    |
        +----------------+
            ▲
            │
            user

Now:

        user is another

Python says:

    True

because there is only one dictionary.

But suppose someone creates:

    {
        "name": "Taki"
    }

again.

Now there are two dictionaries.

Same content.

Different objects.

Equality:

    True

Identity:

    False


Think Like an Engineer

When should we care about equality?

When comparing values.

Example:

    password == entered_password

We don't care whether they are literally the same object.

Only whether the text matches.

When should we care about identity?

When asking:

Is this literally the exact same object?

Examples:

shared tensors
caching
singleton objects
None
object ownership
memory optimization
One Very Important Rule

You will often see this:

    if value is None:

Notice:

is

Not:

    if value == None:

Why?

Because there is only one None object in Python.

You're asking:

    Is this object literally the singleton None?

We'll study this much later, but remember the rule now:

    Always use is None and is not None.

Under the Hood

Conceptually:

Equality (==) asks:

    Object A

    ↓

    Compare Value

    ↓

    Object B

Identity (is) asks:

    Address A

    ↓

    Compare Address

    ↓

    Address B

Same value?

Use ==

Same object?

Use is

## Common Beginner Mistake

Many beginners write:

if x is 5:

This is wrong.

Why?

Because you're asking:

Is this literally the same object?

When what you really mean is:

Does this equal 5?

Correct:

if x == 5:

## Why This Matters for AI

Suppose:

tensor2 = tensor1

If you ask:

tensor1 is tensor2

You're asking:

Are these two names sharing the same tensor in memory?

That's extremely important when training neural networks.

Sometimes you want a copy.

Sometimes you want shared memory.

Knowing the difference prevents subtle bugs and wasted memory.

## Summary

compares values
asks "Do these represent the same information?"

is

compares identity
asks "Are these the exact same object?"


Supervisor's Challenge

At the end of these exercises, I'm going to bring back the question I asked you earlier:

x = 10
y = x
x = 20

This time, you'll have the tools to explain exactly what happens to the objects, the names, and their identities.

If you can explain that correctly without executing the code, it will show you've started thinking like the Python runtime rather than like a person reading source code.


