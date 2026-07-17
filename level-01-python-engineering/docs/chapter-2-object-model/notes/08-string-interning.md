# Lesson 8 — String Interning
## The Problem

Imagine you're one of the engineers building Python.

One day you profile thousands of Python programs.

You notice something interesting.

These strings appear everywhere:

"name"
"email"
"id"
"GET"
"POST"
"username"
"password"
"class"
"def"
"return"

Every program creates them.

Sometimes millions of times.

Now imagine this program:

    user1 = "admin"
    user2 = "admin"
    user3 = "admin"
    user4 = "admin"

Question:

Should Python create

Heap

"admin"
"admin"
"admin"
"admin"

Four identical objects?

Or should it create

            "admin"
          /    |    \
         /     |     \
     user1  user2  user3
                   |
                user4

Only one object?

Think Like a Language Designer

Before we continue...

Ask yourself:

Why did Python cache small integers?

Because:

they're used constantly
they're immutable
sharing is safe
creating objects costs memory and CPU

Now ask yourself:

Are strings...

used constantly?
immutable?
expensive to create?

The answer is yes to all three.

So if you were designing Python...

Would you also reuse some strings?

The Answer

Yes.

Python has an optimization called String Interning.

Interning means:

Instead of creating multiple identical immutable string objects, Python may keep a single shared object and let every variable point to it.

Visualizing It

Without interning:

Heap

    +---------+
    | "admin" |
    +---------+

    +---------+
    | "admin" |
    +---------+

    +---------+
    | "admin" |
    +---------+

Three separate objects.

With interning:

             Heap

        +-----------+
        | "admin"   |
        +-----------+
          ^    ^    ^
          |    |    |
         x     y    z

One object.

Three names.

Much less memory.

## Why Is This Safe?

Because strings are...

Immutable.

You cannot do this:

name = "admin"

name[0] = "A"

Python refuses.

Since nobody can modify "admin",

millions of variables can safely share it.

Exactly the same reasoning we used for small integers.

Wait...

Does Python Intern Every String?

Now think like an engineer again.

Suppose Python interns

every string ever created.

Imagine a web server.

Users upload:

Invoice_348294.pdf

IMG_2026_07_17_184923.png

VeryLongRandomPassword1239487234987234

SessionID_8923479823479823479823

Millions of unique strings.

Should Python keep all of them forever?

Probably not.

Memory would explode.

## So Which Strings Get Interned?

Python mainly interns strings that are good candidates for reuse.

Examples include:

identifiers
variable names
attribute names
many short constant strings
many compile-time literals

Examples:

username = "admin"

status = "active"

method = "GET"

These are likely to be interned.

Random strings generated at runtime often are not.

## Why Not Intern Everything?

Suppose every uploaded filename were interned forever.

photo_001.png

photo_002.png

photo_003.png

...

photo_9000000.png

Nobody will ever reuse most of them.

Interning them wastes memory instead of saving memory.

Optimization becomes a pessimization.

Good optimizations solve common problems—not every possible one.

Comparing Identity

Suppose:

a = "hello"

b = "hello"

Sometimes:

a is b

returns

True

because both names point to the same interned object.

But now imagine:

a = "Hello, my name is Taki and I like building AI systems."

b = "Hello, my name is Taki and I like building AI systems."

Depending on how the string is created and the Python implementation, these may or may not be the same object.

Again:

Never rely on is for string equality.

## Equality vs Identity (Again)

Correct:

username == "admin"

Wrong:

username is "admin"

Why?

Because you're asking different questions.

==

asks

Do these strings contain the same characters?

is

asks

Are these literally the same object?

Almost always,

you care about the first question.

## Relationship to Small Integer Caching

Notice something beautiful.

Small Integer Caching:

Many identical integers

↓

Reuse one object

String Interning:

Many identical immutable strings

↓

Reuse one object

Same idea.

Different object type.

## The General Principle

You're beginning to see one of Python's design philosophies.

Whenever an object is:

immutable
commonly reused
expensive to recreate

Python may choose to share it.

Not because the language requires it.

Because it's an excellent optimization.

## Real AI Example

Imagine an NLP pipeline.

Millions of documents contain:

the

and

is

of

to

Should Python allocate millions of separate "the" objects?

Or reuse one?

Reusing immutable strings dramatically reduces memory usage.

This matters when processing gigabytes of text.

Another Real Example

Suppose you're processing one billion JSON records.

Every record contains:

    {
        "id": ...,
        "name": ...,
        "email": ...
    }

Without interning:

"id"

"id"

"id"

"id"

"id"

Millions of duplicate objects.

With interning:

One "id" object.

Millions of references.

Huge memory savings.

Important Rule

Never write code that depends on string interning.

Write:

if command == "exit":

Not:

if command is "exit":

One expresses your intent.

The other depends on an implementation optimization.

## Mental Model

Think of immutable objects as library books.

If ten students want to read the same mathematics textbook,

the university doesn't print ten identical books every minute.

It buys one copy (or a reasonable number of copies) and lets many students refer to it.

Sharing works because nobody is allowed to permanently write inside the book.

If everyone could freely edit the pages,

sharing would become impossible.

That's exactly why immutability enables safe sharing.

Key Takeaways

String interning is an optimization that allows identical immutable strings to be shared.

It reduces memory allocations and improves performance.

Python does not intern every string.

Interning is an implementation optimization, not something your code should depend on.

Always use == to compare string values.

Use is only when you genuinely care about object identity (for example, with None).
