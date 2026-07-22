# Lesson 4 — Numeric Tower

Let's start with something surprising.

print(True + True)

Output:

2

Now:

print(True * 10)

Output:

10

Now:

print(False + 5)

Output:

5

If you came from many other languages, this might look strange.

### Why can you add booleans to integers?

First Thought

You might think:

Python secretly converts True into 1.

That explanation is incomplete.

Python isn't performing a special conversion here.

The truth is even more interesting.

## The Real Reason

In Python,

### bool is a subclass of int.

Let's verify.

    print(isinstance(True, bool))

Output:

True

No surprise.

Now:

print(isinstance(True, int))

Output:

True

Wait...

How can True be both a bool and an int?

The Numeric Hierarchy

Conceptually:

object
   │
 number
   │
   ├── int
   │      │
   │      └── bool
   │
   ├── float
   │
   └── complex

Don't worry about every detail yet.

The important relationship is

int
│
└── bool

A boolean is a specialized integer.

Why?

Computers already represent truth as

1
0

Python embraces this.

Instead of inventing a completely unrelated type,

it specializes integers.

Internally,

True

behaves numerically like

1

and

False

behaves like

0

while still printing

True
False

to make programs readable.

Let's explore
print(int(True))

Output:

1

Now:

print(int(False))

Output:

0

Notice something.

We're not converting random objects.

We're asking the bool object to express itself as an integer.

Because it already is one.

More Examples
5 + True

Conceptually becomes

5 + 1

Result:

6
8 * False

Conceptually becomes

8 * 0

Result:

0
Why Python Did This

Imagine counting successful predictions.

Instead of writing

correct = 0

if prediction == answer:
    correct += 1

you can write

correct += prediction == answer

Why?

Because

prediction == answer

produces either

True

or

False

which contribute

1 or 0

This makes many algorithms elegant.

AI Engineering Example

Suppose you're evaluating a classifier.

predictions = [True, False, True, True]

You want accuracy.

Instead of

count = 0

for p in predictions:
    if p:
        count += 1

Python allows

accuracy = sum(predictions)

because

True  = 1
False = 0

If there are

True
False
True
True

then

1 + 0 + 1 + 1 = 3

This idea appears constantly in machine learning libraries.

Numeric Promotion

Python also knows how to combine different numeric types.

Example:

5 + 2.5

Output:

7.5

What happened?

Python promoted the integer.

Conceptually:

int

↓

float

because

a float can represent everything an integer can,

but not the other way around.

Another example

3 + 4j

Output:

(3+4j)

The integer becomes compatible with the more expressive numeric type.

Python automatically promotes values when necessary.

The Numeric Tower

Conceptually,

Python prefers moving upward rather than downward.

bool

↓

int

↓

float

↓

complex

Each level can represent more kinds of numbers.

Memory Model

Consider

x = True

Memory:

x
│
▼
True object
│
▼
bool
│
▼
int hierarchy
│
▼
type

Even though

True

acts like

1

it is still a boolean object.

The object keeps its identity.

Important Distinction

These are equal:

True == 1

Output:

True

But this:

True is 1

Output:

False

Why?

Because

equality asks

"Do these represent the same value?"

identity asks

"Are these literally the same object?"

We've already studied this distinction in Chapter 2.

This lesson connects back beautifully to it.

Best Practice

Just because Python allows

True + True

doesn't mean you should write code like this everywhere.

Good engineering values clarity.

This:

correct += prediction == label

is elegant.

This:

result = True * 8 + False

is probably confusing.

Use numeric booleans when they naturally express the problem.

Mental Model

Don't think:

Python converts booleans into integers.

Think:

Booleans are specialized integer objects that participate naturally in numeric operations.

That's a subtle but important distinction.

Looking Ahead

You might now wonder:

If Python cares less about declared types than many languages...

How can a function work with completely different objects as long as they behave similarly?

That question leads us directly to one of Python's core philosophies.

Duck Typing.

