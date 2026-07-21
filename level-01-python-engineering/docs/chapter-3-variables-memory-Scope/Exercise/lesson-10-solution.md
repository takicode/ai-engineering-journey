# Exercises

Since this is the final lesson of the chapter, we'll focus on synthesis rather than repetition.

## Exercise 1 — Following the Chain

In your own words, describe what happens conceptually when Python executes:

numbers = [1, 2, 3]

Starting from the execution frame and ending at the object in memory.

Use the mental model we've built.


Evaluation in the Frame: The active execution frame evaluates the right-hand side of the statement. It requests space in heap memory to construct a brand-new list container object holding three integer objects.

Namespace Registration: The execution frame looks at its own associated namespace (its dictionary of names). It registers the string identifier "numbers" into this local dictionary.

Binding the Reference: Python places a pointer (memory address reference) as the value next to the key "numbers". The name is now bound to the list object, completing the chain from code to memory.

## Exercise 2 — Why Frames Matter

Suppose Python reused the same execution frame for every function call instead of creating a new one.

Explain at least four serious problems this would cause.

Think about:

recursion,
nested function calls,
concurrency,
debugging.

Recursion becomes impossible: A recursive function would overwrite its own local variables on every deeper call. When unwinding the recursion stack, the parent states would be permanently lost.

Nested function calls collapse: If Function A calls Function B, Function B would overwrite Function A's variables inside the shared frame. Function A could not safely resume execution after Function B returns.

Concurrency crashes immediately: If two threads attempt to execute code simultaneously, they would read and write to the exact same frame variables, causing massive data corruption and race conditions.

Debugging is ruined: Stack traces would cease to exist. A debugger could not show you the path of function calls that led to a crash, because previous execution history is actively erased.

## Exercise 3 — The Big Picture (Chapter Reflection)

Without mentioning syntax, explain how these ideas fit together into one coherent model:

Objects
References
Names
Namespaces
Execution Frames
Scope
Object Lifetime

Imagine you're explaining Python's execution model to a new AI engineer who wants to understand what really happens in memory.


1. The Concrete Layer: Objects and Lifetimes
Everything in Python lives in a giant pool of memory called the heap. Data exists only as Objects (integers, strings, lists, functions). An object's Object Lifetime is strictly tied to how many things are pointing to it. It stays alive as long as something holds a reference to it; the moment that count drops to zero, Python's garbage collector purges it from memory.

2. The Connecting Layer: Names and References
Objects do not have names; names live separately from objects. A Name is just a text label. A Reference is the invisible arrow (a memory pointer) connecting that text label to the actual object in the heap.

3. The Structural Layer: Namespaces, Frames, and Scope
When Python runs code, it creates an Execution Frame to serve as the workspace for the current function. Inside this frame sits a Namespace, which is simply a dictionary tracking all local text labels and their references.

Scope is the set of rules Python uses to search through these namespaces. If a name isn't found in the current frame's namespace, the scope rules dictate how Python looks upward through enclosing frames, then the global namespace, and finally the built-in system namespace.