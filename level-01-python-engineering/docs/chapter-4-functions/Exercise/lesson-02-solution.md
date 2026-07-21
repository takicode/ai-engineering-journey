Exercises

As before, don't run the code. Reason from the mental model.

Exercise 1 — Defining vs Calling

In your own words:

What is the difference between defining a function and calling a function?
Which one creates the function object?
Which one creates the execution frame?
Why are these two events completely separate?
Exercise 2 — Following the Timeline

Consider:

print("Start")

def greet():
    print("Hello")

print("Middle")

greet()

print("End")

Without running it, answer conceptually:

At what point is the function object created?
At what point does "Hello" actually execute?
How many execution frames are created for greet()?
Is the function object recreated when greet() is called?
Exercise 3 — AI Engineering Thinking

Imagine a deep learning framework loads this callback:

def save_checkpoint():
    ...

The callback is registered when training starts but isn't called until the end of every epoch.

Explain conceptually:

Why is it useful that defining the function doesn't execute it immediately?
Why can the framework safely store the function object for later?
What problems would occur if def automatically executed the function body?

Take your time. This lesson is simple on the surface, but understanding it deeply will make callbacks, decorators, event systems, and AI frameworks much easier to reason about later.