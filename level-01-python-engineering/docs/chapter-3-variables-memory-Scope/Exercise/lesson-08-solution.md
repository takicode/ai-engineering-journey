Exercises

As before, don't run the code. Reason from the mental model.

Exercise 1 — When Are Default Arguments Created?

In your own words:

When are default argument objects created?
Where are they stored?
Why aren't they recreated every function call?
Exercise 2 — Following the Object

Consider:

def collect(x, items=[]):
    items.append(x)
    return items

Now imagine:

collect(1)
collect(2)
collect(3)

Without running the code, answer:

How many list objects are created?
How many function objects exist?
Why does each call "remember" the previous values?
Which object owns the reference to the default list?
Exercise 3 — Why None Works

Consider the pattern:

def collect(x, items=None):
    if items is None:
        items = []

    items.append(x)
    return items

Explain:

Why does this create a fresh list each time?
When is the new list actually created?
Why doesn't the function object keep reusing it?
Exercise 4 — Architecture Thinking

Imagine an AI preprocessing function:

def preprocess(image, history=[]):
    ...

This function is called millions of times during training.

Conceptually explain:

What kind of bug could this introduce?
Why might the bug be difficult to notice?
Why is this especially dangerous for machine learning experiments?
Exercise 5 — Challenge

A developer says:

"Python should simply recreate default arguments every time a function is called. That would eliminate this problem."

Evaluate this idea.

Discuss the trade-offs in terms of:

performance,
consistency,
immutable defaults,
language design.

Would it solve one problem while introducing others? Why?