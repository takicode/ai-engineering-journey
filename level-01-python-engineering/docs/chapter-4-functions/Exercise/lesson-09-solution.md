Exercises

As always, don't run the code. Reason from the mental model.

Exercise 1 — Why Can Functions Be Passed Around?

In your own words:

Why can Python pass a function as an argument?
What is actually being passed?
Why doesn't passing a function automatically execute it?
Exercise 2 — Function Object vs Function Call

Conceptually compare:

process

and

process()

Explain:

Which one refers to the function object?
Which one creates an execution frame?
Why are they fundamentally different operations?
Exercise 3 — Returning Functions

Suppose a function returns another function.

Without writing code, explain:

What is actually returned?
Does the returned function execute immediately?
Why can the caller store it and execute it much later?
Exercise 4 — AI Engineering Thinking

Imagine you're designing an AI training framework.

Instead of hardcoding behavior, you let users provide:

a logging function,
a checkpoint-saving function,
a learning-rate scheduling function.

Conceptually explain:

why passing functions instead of hardcoding behavior makes the framework more reusable,
why the framework stores function objects instead of executing them immediately,
and how this design allows different users to customize the same training engine without modifying its source code.