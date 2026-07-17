## Lesson 7 — Small Integer Caching
The Mystery

Consider this:

    a = 10
    b = 10

    print(a == b)
    print(a is b)

Output:

True
True

No surprise.

Now this:

    a = 100
    b = 100

print(a is b)

Still:

True

Still okay.

Now:

    a = 256
    b = 256

print(a is b)

Output:

True

Still true.

Now:

    a = 257
    b = 257

print(a is b)

Sometimes:

False

Sometimes:

True

depending on how the code is executed (interactive shell vs. script, optimization, implementation details).

Why?

First Question

Before we answer it, remember this.

Python objects live on the heap.

Creating objects costs:

memory
CPU time
reference counting
garbage collection

Imagine this code:

    x = 1
    y = 1
    z = 1

    a = 2
    b = 2
    c = 2

    ...

Millions of times.

Should Python create

    Object(1)
    Object(1)
    Object(1)
    Object(1)
    Object(1)

every single time?

Or

        1
      / | \
     /  |  \
    x   y   z

using just one object?

Which design do you think is more efficient, and why?

## Why Small Integers?

Think about everyday programs.

How often do we use numbers like:

0
1
2
3
4
5
10
20
100
255

Very often.

Now think about:

987654321
-824632
12345678901234567890

Much less often.

Python's designers noticed something.

Tiny integers are created constantly.

Examples:

for i in range(100):
    ...

Every loop uses integers.

Indexes:

items[0]
items[1]
items[2]

Lengths:

len(name)

Booleans become integers internally in some contexts:

True == 1
False == 0

Counters:

count += 1

Everything uses small numbers.

Creating new objects for them would waste enormous amounts of memory.

## The Optimization

When CPython starts,

it creates integer objects for

-5
-4
-3
...
255

only once.

Think of them as permanent residents.

Heap

Integer -5
Integer -4
...
Integer 0
Integer 1
Integer 2
...
Integer 255

These objects stay alive for the lifetime of the Python interpreter.

Whenever you write

x = 5

Python does not create a new integer object.

Instead:

            Integer 5
           /    |    \
          /     |     \
         x      y      z

Every variable simply points to the same cached object.

## Why Only Small Integers?

Imagine Python cached every integer ever created.

1
2
3
4
...

999999999999999999999999999

Memory would grow forever.

Terrible idea.

Instead,

Python caches only the values that are used constantly.

## Why This Doesn't Break Immutability

Remember:

Integers are immutable.

Nobody can change

5

into

7

Therefore it's perfectly safe for millions of variables to share one object.

If integers were mutable...

x → 5
y → 5
z → 5

and

x += 1

actually changed the object...

everyone would suddenly become

6

Chaos.

Immutability makes sharing safe.

Visual Memory Diagram

Cached Integer Objects

          Heap

      +-----------+
      | Integer 5 |
      +-----------+
        ^   ^   ^
        |   |   |
        x   y   z

One object.

Three references.

Reference count = 3 (ignoring internal references).

Another Example
a = 100

b = 100

c = 100

Memory:

           Integer 100

          /     |      \
         a      b       c

Still one object.

Larger Numbers

a = 100000

b = 100000

Python is not required to reuse the object.

It may create

a ----> Integer 100000

b ----> Integer 100000

Two distinct objects with the same value.

So:

a == b

True.

But

a is b

may be False.

This is why is should never be used to compare numbers or strings for equality.

Why You Should Almost Never Use is

Correct:

username == "admin"

Wrong:

username is "admin"

Correct:

age == 18

Wrong:

age is 18

The is operator asks:

"Are these the exact same object?"

Most of the time, what you really want is:

"Do these objects have the same value?"

## The One Major Exception

There is one singleton object in Python:

None

There is exactly one None object.

So this is correct:

if value is None:
    ...

Not:

if value == None:
    ...

We'll explain singleton objects later in the course.

Key Takeaways
CPython pre-creates integer objects from -5 to 256.

These cached integers are reused throughout the interpreter.

This saves memory and avoids creating millions of identical objects.

The optimization is safe because integers are immutable.

Larger integers are not guaranteed to be cached.

Never use is to compare numbers or strings for equality.

Use is primarily for identity checks (such as None).

