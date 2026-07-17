## Exercise 1

In your own words:

What does rebinding mean in Python?

How is it different from changing an object?

Rebinding means moving a variable name from one memory object to a completely different memory object. The objects themselves do not alter; you are simply changing what the name points to.

Changing an object (mutating) means modifying the internal data inside an existing object while the variable name stays attached to that exact same memory identity.

## Exercise 2

Consider:

x = 5

y = x

x = 8

Draw the memory conceptually using ASCII.

How many objects exist?

How many names exist?

Which object does each name point to?


    Names (Variables)         Memory Objects
    +---------------+         +--------------+

    |       x       | ------> |  Integer 8   |
    +---------------+         +--------------+
    
    +---------------+         +--------------+

    |       y       | ------> |  Integer 5   |
    +---------------+         +--------------+

Counts and Assignments
Objects existing: 2 integer objects exist (5 and 8).
Names existing: 2 names exist (x and y).
Pointers: The name x points to the object 8. The name y points to the object 5


## Exercise 3

Why doesn't executing:

x = 20

change the integer object 10 into 20?

Why is creating a new object a safer design?


Executing x = 20 does not change the original object 10 because integers in Python are immutable (unchangeable). The object 10 is a fixed, permanent piece of data in memory for as long as it exists.

Creating a new object is a much safer design because it prevents accidental side effects. If changing x physically altered the number 10 into 20, every other variable in your entire program that happened to point to 10 (like a price, an index, or a score) would suddenly and silently change to 20 as well, breaking the program.

## Exercise 4

Suppose:

a = "Python"

b = a

c = b

b = "AI"

Without using id() or running the code:

How many string objects exist at the end?
Which names point to each object?
Did any string object change?

Explain your reasoning.


String objects existing at the end: 2 string objects ("Python" and "AI").

Name mappings: a and c point to "Python". b points to "AI".

Did any object change? No. Strings are immutable; they cannot be changed.

Reasoning Step-by-Step:
a = "Python" creates the "Python" object. Name a points to it.b = a and c = b attach names b and c to that exact same "Python" object. All three names share one identity.

b = "AI" evaluates the right side, creates a brand new "AI" object, and rebinds the label b to it. Names a and c are completely unaffected and remain bound to "Python".

## Exercise 5 (Thinking)

Imagine assignment automatically copied every object instead of rebinding names.

Name at least four serious problems this would cause for:

memory usage,
performance,
AI workloads,
large datasets,
function calls.

Memory Exhaustion (AI Workloads): Loading an 80 GB large language model into model_1 and writing model_2 = model_1 would force Python to copy all 80 GB of weights, instantly crashing the system with an out-of-memory error.

Extreme CPU Bottlenecks (Performance): Passing a large dataset to a function would trigger a mandatory copy of every row and column. The CPU would spend more time physically moving bytes around in RAM than actually processing data.

Broken Function Modifications (Function Calls): If you pass a large database cache list into a function to clean up old entries, the function would receive a copy. The function would clean the copy, and the original dataset outside the function would remain bloated and unchanged.

Data Desynchronization (Large Datasets): Tracking real-time updates across a system would fail. If multiple parts of an application need to look at a shared configuration dataset, making a change in one place would not reflect anywhere else because every component would be holding an isolated, outdated copy.

## Exercise 6 (Challenge)

A student says:

"When I execute x = 20, Python changes the value stored inside x."

Write a response that corrects this misunderstanding.

Do not simply say "variables are references."

Explain, step by step, what actually happens in memory.


"I see why it looks like x is a box holding a value that changes, but Python handles memory differently.When you run x = 20, Python does not look inside x and overwrite a number. Instead, here is what happens step by step:Python looks at the right side (20) and builds a completely fresh, separate integer object representing 20 in a new spot in memory.Python looks at the name x on the left side.Python unties the x label from whatever object it was pointing to previously.Python snaps the x label onto the brand-new 20 object.The old object isn't modified at all; x has just been given a new assignment."


