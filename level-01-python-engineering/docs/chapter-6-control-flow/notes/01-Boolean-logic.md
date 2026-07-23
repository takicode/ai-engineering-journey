# Lesson 1: Boolean Logic

This chapter is not about memorizing if statements.

It's about understanding how Python makes decisions.

Every AI system eventually boils down to questions like:

    Is the model finished training?
    Is the validation loss improving?
    Is the prediction confidence high enough?
    Should this request be accepted?
    Has this user authenticated?

All of these are decisions.

Python makes every one of those decisions using Boolean logic.

## What is a Boolean?

A Boolean is the simplest possible type of information.

It answers only one question:

    True or False?

Python has exactly two Boolean objects:

True
False

Not "maybe."

Not "almost."

Not "1.5."

Only:

True
False

Booleans Are Objects

Remember Chapter 5:

Everything in Python is an object.

That includes Booleans.

    flag = True

Conceptually:

    flag
     │
     ▼
    True Object

flag is just a name.

True is the object.

The bool Type

Just like:

int
float
str
list

there is also

bool

You can create Boolean values explicitly:

    is_admin = bool(1)

    is_logged_in = bool("")

We'll soon understand why these produce different results.

## Where Do Booleans Come From?

Sometimes we write them directly.

finished = True

But much more commonly...

Python computes them.

Example:

    age = 18

    age >= 18

Python evaluates the expression.

The result is not another integer.

The result is:

    True

Another example:

    temperature = 32

    temperature < 0

Result:

    False

The comparison itself produces a Boolean object.

## Comparison Operators

These operators ask questions.

    ==
    !=
    <
    >
    <=
    >=

Examples:

    5 > 3

      ↓

    True


    10 < 7

      ↓

    False


    8 == 8

      ↓

    True

    8 != 8

      ↓

    False

Notice something important.

These operators don't change objects.

They evaluate relationships between objects.

## Identity vs Equality (Review)

From Chapter 2:

    ==

asks:

"Do these objects have the same value?"

while

    is

asks:

"Are these the exact same object?"

Those produce Booleans too.

Example:

    a = [1]

    b = [1]

Then:

    a == b

      ↓

    True

because the values match.

But

    a is b

      ↓

    False

because they are different objects.

## Boolean Operators

Sometimes one comparison isn't enough.

Python provides:

    and
    or
    not

Suppose:

    age = 25

Then:

    age > 18 and age < 65

asks:

    Is BOTH true?

If yes:

    True

Suppose:

    is_admin = False

    is_owner = True

Then:

    is_admin or is_owner

asks:

    Is AT LEAST ONE true?

Result:

True

Finally:

    not True

    ↓

    False

and

    not False

    ↓

    True

It simply reverses the answer.

## Think Like a Decision Tree

Imagine an AI moderation system.

    Message arrives

         ↓

    Is user authenticated?

        ↓

    True?

      ↓

    Yes

     ↓

    Is message safe?

        ↓

    True?

      ↓

    Publish

Every branch is based on Boolean values.

Not integers.

Not strings.

Booleans.

### AI Example

Suppose you're training a model.

loss = 0.03

You ask:

    loss < 0.05

Python evaluates that expression.

The result is:

    True

Then your code might decide:

Stop training.

Again,

the comparison returns a Boolean,

and the Boolean drives the decision.

## The Mental Model

Python executes:

    accuracy > 0.95

like this:

    Look up accuracy.
    Retrieve the object.
    Compare its value to 0.95.
    Produce either the True object or the False object.
    Return that Boolean object.

Notice:

Comparisons create new Boolean results.

They don't modify the numbers being compared.

## Why This Matters

In the coming lessons we'll study:

    if

But if doesn't understand numbers.

It doesn't understand strings.

It only understands one thing:

A Boolean answer.

Everything else eventually becomes one.

That's why Boolean logic comes first.
