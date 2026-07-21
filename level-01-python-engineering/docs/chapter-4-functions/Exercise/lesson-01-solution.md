Exercises

Exercise 1 — The Mental Model

In your own words:

Why is a function an object instead of just "code"?
What does the def statement actually do conceptually?
Is greet the function, or is it something else?
Why doesn't the function body execute when Python reaches the def statement?

Why a function is an object: A function is an object because it needs to be manipulated dynamically during runtime. Just like a list or a dictionary, a function can be passed as an argument, assigned to new variables, and stored inside data structures. "Code" is just a static recipe; a function object is a live entity in memory that wraps that recipe along with its execution context (like its enclosing scope).

What def actually does: Conceptually, def is an assignment statement. It is a factory line that bundles compiled bytecode, a reference to the current environment, and metadata into a new function object on the heap. Then, it binds that object to a name in the current namespace.

Is greet the function? No. greet is simply a name (a text pointer). The function is the independent object sitting in heap memory. greet just happens to hold the reference that points to it.

Why the body doesn’t execute: The def statement is a definition phase, not an execution phase. Python reads the body solely to compile it into a frozen block of bytecode to store inside the function object. It does not open a runtime frame to execute those lines until the function object is explicitly called using ().

Exercise 2 — Memory Reasoning

Without running the code:

def add(a, b):
    return a + b

Conceptually answer:

How many function objects exist after this definition?
Where is the function object stored?
Where does the name add live?
What information do you think the function object contains besides the executable code?
What doesn't happen until someone calls add(...)?



How many function objects exist: Exactly one function object exists.

Where the function object is stored: It is stored in heap memory, alongside all other objects like lists, strings, and integers.

Where the name add lives: The name add lives in the namespace dictionary of the execution frame where the def statement was run (e.g., the global namespace if written at the top level of a module).

What else the function object contains: Beyond bytecode, it holds critical metadata:__name__: The original name string ("add").__globals__: A direct pointer back to the global namespace dictionary where it was defined (so it knows where to look for global variables later).__defaults__: Storage for any default argument values.__doc__: The docstring, if provided.

What doesn't happen until a call: Python does not create an execution frame for the function, does not allocate local namespace memory, and does not evaluate or bind the parameter names (a and b) to any real data until add(...) is explicitly called.

