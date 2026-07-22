Exercises

As always, don't run the code. Build the answer from the mental model.

Exercise 1 — One Function, Many Frames

In your own words:

Why doesn't recursion create multiple function objects?
What gets created instead?
Why can several calls to the same function exist simultaneously?
Exercise 2 — Following the Stack

Consider:

def count(n):
    if n == 0:
        return

    count(n - 1)

count(3)

Without running it, answer:

Which frame is created first?
Which frame is on top when n == 0?
Which frame disappears first?
Which frame disappears last?
Exercise 3 — Why the Base Case Matters

A student says:

"The base case is there so the function knows what answer to return."

Evaluate this statement.

Explain:

the deeper reason recursion needs a base case,
what happens to the call stack without one,
why Python eventually raises RecursionError.
Exercise 4 — AI Engineering Thinking

Imagine you're writing a function that recursively walks through a directory containing millions of training images organized into nested folders.

Conceptually explain:

why each recursive call gets its own execution frame,
why each frame needs its own local variables,
how the call stack allows Python to return to the correct parent folder after finishing a subfolder,
and why extremely deep directory nesting could eventually cause a recursion limit error.