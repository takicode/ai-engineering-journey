Exercises
Exercise 1

In your own words:

What problem does a compiler solve?

Exercise 2

What problem does an interpreter solve?

How is it different from a compiler?

Exercise 3

Why does Go usually produce an executable file, while Python usually doesn't?

Exercise 4

Conceptually, what is bytecode?

Why do you think Python uses it?

Exercise 5

Which statement is more accurate?

A.

Python is interpreted.

B.

CPython compiles Python source code into bytecode, which is then executed by the Python Virtual Machine.

Explain why.

Exercise 6 (Thinking)

Suppose Python were changed tomorrow so that it compiled directly into machine code like Go.

What advantages might that bring?

What Python features might become more difficult to support?

Exercise 7 (Challenge)

Imagine you write an AI model in Python.

Most of the time is spent multiplying huge matrices.

Why can Python still be fast even though Python itself isn't compiled directly into native machine code?

Think carefully. This question connects today's lesson with everything you've learned about abstraction layers.


Exercise 8 

Imagine two people write the exact same AI algorithm:

Person A writes it in pure Python.
Person B writes the performance-critical parts in C and exposes them to Python.

Why will Person B's version often be dramatically faster, even though both are "using Python"?

Don't answer with:

"Because C is faster."

That's a conclusion.

I want the chain of reasoning—from source code, through compilation or interpretation, all the way to the CPU.

That style of explanation is what separates someone who knows from someone who understands.

