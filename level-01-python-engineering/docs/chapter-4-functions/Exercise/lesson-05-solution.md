# Exercises

As always, don't run the code. Build the answer from the mental model.

## Exercise 1 — The Passing Model

In your own words:

Why isn't Python accurately described as pass-by-reference?
Why isn't it accurately described as pass-by-value?
What does pass-by-object-sharing mean?

Why it is not traditional pass-by-reference: In a strict pass-by-reference system, the function receives a reference to the caller's variable slot itself. If you assign a new object to the local variable inside the function, the caller's variable changes its target outside the function too. Python cannot do this; assigning a new value locally merely breaks the local connection without altering the caller's variable.

Why it is not traditional pass-by-value: In a pass-by-value system, Python would copy the entire underlying data object before handing it over to the function. If you changed or mutated that data inside the function, the caller's original data would remain untouched. Python doesn't do this; it passes the actual object, meaning changes to mutable objects are instantly visible to the caller.

What pass-by-object-sharing means: It means Python evaluates the argument expression to an object, then binds the parameter name to that same object in the new execution frame. The function does not get a copy of the object, nor does it get a link to the caller's variable name. It simply receives a shared, independent pointer that points to the exact same shared object sitting on the heap.

## Exercise 2 — Mutation vs Rebinding

Consider:

def process(data):
    data.append(4)

and

def process(data):
    data = [4]

Conceptually explain:

What is identical about the beginning of both function calls?
At what point do their behaviors become different?
Which one mutates an object?
Which one only changes a local name?
Why does only one affect the caller?


What is identical at the beginning: Both functions receive the exact same 8-byte memory reference pointing to the caller's original object. Both functions start with a local execution frame where the local name data points directly to that shared heap object.

The turning point: Their behaviors diverge on the very first line inside the function body based on whether they use an operator/method or an assignment statement (=).

Which one mutates an object: data.append(4) mutates the object. It follows the pointer to the existing list container on the heap and modifies its internal structure.

Which one only changes a local name: data = [4] only changes the local name. The assignment operator creates a brand-new list object on the heap and updates the local name data to point to this new object.

Why only one affects the caller: The first example updates the shared object that the caller is still watching. The second example merely cuts the local connection to the shared object and points the local name somewhere else, leaving the caller's original object completely untouched on the heap.

Exercise 3 — Following the Objects

Suppose:

items = [1, 2]

process(items)

Without running code, explain the complete sequence from:

the caller evaluating items,
to the function receiving its parameter,
to the parameter becoming a local variable,
to both names referring to the same object.

Describe it as a timeline rather than individual facts.


The caller evaluates items: The interpreter looks up the name items in the caller's namespace dictionary and retrieves its associated heap memory address pointer.

The function receives its parameter: Python matches the evaluated memory pointer against the positional slots defined in the function signature.

The parameter becomes a local variable: Python spawns a brand-new execution frame for process. In this frame's local namespace dictionary, it creates a new entry key string "data".

Both names refer to the same object: Python writes the incoming memory pointer value directly next to the local key "data". At this exact moment, the global name items and the local name data coexist as distinct aliases pointing to the identical list object in heap memory.

Exercise 4 — AI Engineering Thinking

A junior AI engineer says:

"Calling train(model) duplicates the model in RAM."

Evaluate this statement.

Explain:

what actually happens,
why Python was designed this way,
why this design is essential for training and inference on large neural networks,
and what would happen if Python instead copied every model during every function call.


Evaluation of the Statement - The junior engineer's statement is completely incorrect. Calling train (model) does not copy, duplicate, or clone the model weights in RAM whatsoever.

What Actually Happens - Python passes a single, lightweight object reference (an 8-byte pointer) into the train function's execution frame. The local name inside the training function points directly back to the original model structure residing in memory.

Why Python Was Designed This Way python manages all data as objects on a heap, accessed via references. This design decouples data scale from execution overhead. Whether an object is a single integer or a massive neural network containing billions of parameters, passing it into a function always costs the exact same trivial amount of CPU time and memory: just copying a tiny memory pointer.

Why This is Essential for AI FrameworksLarge language models and deep neural networks easily consume tens or hundreds of gigabytes of VRAM/RAM. Because Python passes by object sharing, frameworks like PyTorch, TensorFlow, and JAX can effortlessly pass giant tensor graphs between compilation wrappers, optimization steps, and evaluation loops instantly. It allows functions to manipulate underlying hardware buffers directly without copying data.

What Would Happen If Python Copied Models- Immediate System Crashes: Running a training loop would cause instantaneous Out-Of-Memory (OOM) errors. The system would attempt to duplicate gigabytes of weights on every single function call, exhausting system memory.

Catastrophic Latency: The CPU and PCIe bus would spend almost all their cycles copying massive arrays of numbers back and forth through memory, bringing training and inference speeds down to an absolute crawl.