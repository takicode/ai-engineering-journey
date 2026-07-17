# Lesson 5 — Reference Counting
The Big Question

So far we've learned:

x = 10

Python creates an integer object.

Then:

x = 20

Python creates another integer object and rebinds x.

That raises a question.

What happened to the object 10?

## Did Python leave it in RAM forever?

If every object stayed in memory forever, every Python program would eventually consume all available RAM.

So something must be cleaning up objects.

That "something" starts with Reference Counting.

## What is a Reference?

You already know that a variable is just a name pointing to an object.

    x
    │
    ▼
    +------+
    |  10  |
    +------+

That arrow is called a reference.

One arrow = one reference.

Example 1

x = 10

Memory

Reference Count = 1

    x
    │
    ▼
    +------+
    |  10  |
    +------+

Only one name points to the object.

Reference count = 1

Example 2

x = 10

y = x

Now

Reference Count = 2

    x───┐
        │
        ▼
    +------+
    |  10  |
    +------+
        ▲
        │
    y───┘

Two names.

One object.

Reference count = 2

Notice something important:

Python did not create another integer.

It simply created another reference.

Example 3

Now

x = 20

Memory becomes

Reference Count of 10 = 1

    y
    │
    ▼
    +------+
    |  10  |
    +------+

Reference Count of 20 = 1

    x
    │
    ▼
    +------+
    |  20  |
    +------+

The object 10 lost one reference.

The object 20 gained one reference.

Example 4

Now

y = 30

Memory

x
 │
 ▼
+------+
|  20  |
+------+

y
 │
 ▼
+------+
|  30  |
+------+

What happened to the object 10?

Nobody points to it anymore.

Its reference count became

0
The Rule

When an object's reference count becomes zero, Python knows:

"Nothing can ever use this object again."

So it can safely reclaim that memory.

This is why Python programs don't continuously consume RAM forever.

## A Real-Life Analogy

Imagine a shared office document.

Project Plan

Alice has a shortcut.

Bob has a shortcut.

Carol has a shortcut.

Project Plan

↑
Alice

↑
Bob

↑
Carol

Three shortcuts.

Reference count = 3.

Alice deletes her shortcut.

Reference count = 2.

Bob deletes his.

Reference count = 1.

Carol deletes hers.

Reference count = 0.

Now nobody can reach the document anymore.

The system is free to delete it.

Exactly what Python does.

References Can Increase

    a = [1, 2, 3]

Count = 1

Now

b = a

Count = 2

Now

c = b

Count = 3

Still only one list exists.

    a ─┐
    b ─┼────► [1,2,3]
    c ─┘

References Can Decrease

    a = [1,2,3]
    b = a

Count = 2

Now

b = None

Count becomes 1.

Now

a = None

Count becomes 0.

The list can now be destroyed.

Why Python Uses Reference Counting

Imagine an AI application creating millions of temporary objects every second.

Without a way to know when an object is no longer needed:

RAM usage would grow indefinitely.
Programs would eventually crash due to running out of memory.
Long-running services (like web APIs or AI agents) would become unstable.

Reference counting provides a simple and immediate way to reclaim many objects as soon as they are no longer reachable.

## One Important Note

Reference counting handles most memory cleanup, but not all.

There is one situation where it fails:

    Object A
    │
    ▼
    Object B

    ▲      │
    │      ▼

    Object A

Both objects reference each other.

Even if nothing else in the program points to them, each still has a reference count greater than zero.

This is called a ``reference cycle,`` and it's the reason Python also has a `Garbage Collector`, which will be our next lesson.

Key Takeaways

A reference is a name (or another object) pointing to an object.
Every object keeps track of how many references point to it.
Creating a new reference increases the count.
Rebinding or deleting a reference decreases the count.
When the count reaches zero, the object can be reclaimed.
Reference counting is fast and automatic, but it cannot detect cyclic references.




