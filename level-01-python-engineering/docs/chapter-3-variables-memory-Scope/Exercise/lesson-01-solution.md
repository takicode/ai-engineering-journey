Exercises

As always:

Don't run code.
Reason from the mental model.
Exercise 1

In your own words:

What is a namespace?

Do not simply say "it's a dictionary."

Explain what problem it solves.

Exercise 2

Suppose:

x = 10
y = [1, 2]
name = "Taki"

Conceptually draw the memory using ASCII.

Show:

the namespace
the heap
the references
Exercise 3

Suppose:

x = 10
y = x

Answer:

How many names exist?
How many objects exist?
Where are the names stored?
Where is the integer stored?
What is shared?
Exercise 4

Suppose:

def greet():
    pass

Conceptually explain:

What object gets created?
What name gets created?
Where is each one stored?
Exercise 5 (Thinking)

Imagine Python had no namespaces.

When you wrote:

print(score)

How would Python find the object?

Why would this become impractical for large programs?

Exercise 6 (Challenge)

A student says:

"Variables are stored in RAM, so Python just searches RAM until it finds the variable name."

Write a response correcting this misunderstanding.

Explain:

what is actually stored in RAM,
what a namespace stores,
why dictionary lookup is dramatically more efficient than searching memory,
and how this design supports large applications and AI systems.