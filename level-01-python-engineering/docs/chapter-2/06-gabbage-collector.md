# Lesson 6 — Garbage Collection
Review

In the last lesson we learned:

An object keeps a reference count.

Example:

    x = [1, 2, 3]

Memory

    x
    │
    ▼
    +-----------+
    | [1,2,3]   |
    | Ref = 1   |
    +-----------+

Now

y = x

Memory

    x ──┐
        ▼
    +-----------+
    | [1,2,3]   |
    | Ref = 2   |
    +-----------+
        ▲
    y ──┘

Later

x = None

Reference count becomes

1

Later

y = None

Reference count becomes

0

Python immediately frees the object.

Everything looks perfect.

So why do we need another memory manager?

## The Problem

Reference counting has one fatal weakness.

It cannot detect cycles.

Example

Imagine two objects.

Object A

Object B

Now

    A
    │
    ▼
    B

    ▲
    │


and

    A → B
    ↑   ↓
    └───┘

Each object points to the other.

Imagine this Python code:

class Person:
    pass

alice = Person()

bob = Person()

alice.friend = bob

bob.friend = alice

Memory

    alice
    │
    ▼

    +---------+
    | PersonA |
    +---------+
        │
        ▼

    +---------+
    | PersonB |
    +---------+
        ▲
        │
        └─────────────

Now imagine

alice = None
bob = None

You might think

"Everything should disappear."

Not quite.

What happens?

The names disappear.

alice

bob

are gone.

But

    PersonA
        │
        ▼
    PersonB

    ▲
    │
    └────────bob

still exists.

Person A references Person B.

Person B references Person A.

Reference counts become

Person A

Ref = 1
Person B

Ref = 1

Neither reaches zero.

Reference counting says

"Someone is still using these."

But nobody actually is.

The objects have become unreachable, yet they keep each other alive.

This is called a reference cycle.

Why This Is Dangerous

Imagine a web server handling

1,000,000

requests.

Every request accidentally creates one cycle.

Request 1

    cycle

    ↓

    never freed

Request 2

    cycle

    ↓

    never freed

Eventually

RAM

██████████████

fills up.

Server crashes.

Enter the Garbage Collector

Python has another system.

The Garbage Collector (GC).

Its job is to find objects that:

still have references,
but cannot actually be reached anymore.

Think of a City

Imagine houses connected by roads.

    House A

    ↓

    House B

Now imagine

A ↔ B

The two houses still have roads between them.

But suppose every road from the city into those houses disappears.

CITY

(no roads)

A ↔ B

The houses still connect to each other.

But nobody can ever reach them.

The Garbage Collector says

"These houses are isolated."

Demolish them.

Exactly what Python does.

Reachability

This is the key idea.

Python doesn't ask

"Does this object have references?"

It asks

"Can this object still be reached from a live part of the program?"

Those are very different questions.

Example

    globals()

    ↓

    config

    ↓

    database

    ↓

    users

Everything is reachable.

Keep them.

Example

    Object A ↔ Object B

Nothing points to either.

Not reachable.

Delete both.

How the Garbage Collector Thinks

Conceptually, it does something like this:

    Start

    ↓

    Look at every live root

    ↓

    Walk through every reference

    ↓

    Mark everything reachable

    ↓

    Anything unmarked

    ↓

    Delete

This process is commonly described as mark-and-sweep.

Note: CPython combines reference counting with a cyclic garbage collector. At this stage, think of "mark-and-sweep" as the conceptual model for how unreachable cycles are identified.

Reference Counting vs Garbage Collection

Reference Counting	    Garbage Collection
Immediate cleanup	    Periodic cleanup
Very fast	             More expensive
Handles most objects    	Handles cycles
Cannot detect circular references	Detects circular references

They work together.

Reference counting cleans up most objects immediately.

The garbage collector periodically cleans up cycles that reference counting cannot resolve.

## Why AI Engineers Should Care

Imagine a training loop.

Every iteration creates

tensors
graphs
metadata
callbacks

Thousands of objects.

If reference cycles accidentally accumulate:

    Iteration 1

    ↓

    memory grows

    Iteration 2

    ↓

    memory grows

    Iteration 100000

    ↓

    OOM

Understanding how objects become unreachable helps diagnose memory growth and leaks in long-running applications.

## Key Takeaways
Reference counting cannot detect circular references.

Circular references keep reference counts above zero.

Objects can be unreachable even if their reference count is not zero.

Python's garbage collector periodically finds and removes unreachable cycles.

CPython uses both mechanisms together.

