# Exercises

As always, don't run the code. Build the answer from the mental model.

## Exercise 1 — What Does return Actually Return?

In your own words:

Does return return a variable?
What does it actually return?
Why is that distinction important?

Does it return a variable: No. Python can never return a variable name or a variable slot.

What it actually returns: It evaluates the expression next to it and returns an object.

Why this distinction is important: If it returned a variable, local variables would leak outside their scope or cause memory errors when their execution frame collapsed. Because it returns an object, Python can seamlessly pass access to the underlying data object across different frames without copying any data.


## Exercise 2 — Following the Timeline

Consider:

    def create():
        data = [1, 2]
        return data

    result = create()

Without running it, explain the complete timeline:

When is the list object created?
When does data become a local variable?
What happens when return data executes?
When does the execution frame disappear?
Why does the list continue to exist afterward?
Which name points to the list after the function finishes?

Creation of the list: The list object is created on the heap during the execution of the first line inside the create() function.

Local variable registration: The name data becomes a local variable instantly when that first line assigns the new list's pointer to it inside create's execution frame.

Executing return data: Python looks up the name data in the local namespace, extracts the 8-byte heap memory pointer, and hands that pointer back to the calling evaluation layer.

Execution frame disappearance: The execution frame for create() collapses and is deleted from the call stack the exact moment the function finishes executing the return.

Why the list continues to exist: An object only dies if its reference count drops to zero. While the local name data vanished with the frame, the pointer was caught and immediately bound to result in the global namespace. The reference count stayed above zero, so the garbage collector left the object intact.

Name pointing to the list at the end: Only the global name result.


Exercise 3 — Returning Large Objects

Suppose:

    def load_model():
        ...
        return model

The model occupies 60 GB of RAM.

Conceptually explain:

Does returning the model duplicate 60 GB?
What is actually returned?
Why is this essential for high-performance AI frameworks?
What would happen if every return copied the entire object?


Does it duplicate 60 GB: No. The model object is never duplicated or copied.

What is actually returned: Just like argument passing, Python returns an 8-byte memory address pointer pointing directly to the model structure on the heap.

Why this is essential: Large language models or deep neural networks take massive chunks of hardware memory. If returning a model required duplication, deep learning frameworks would suffer severe performance penalties and trigger instantaneous Out-Of-Memory (OOM) system crashes due to temporary memory spikes.

What would happen if return copied data: Every time you passed data to a processing wrapper, a loss function, or a checkpoint saver, your machine would completely freeze up or crash trying to continuously replicate gigabytes of weight matrices.


Exercise 4 — The Big Picture

Compare:

train(model)

and

model = load_model()

Explain how argument passing and return values are mirror images of one another.

Describe the complete flow of objects and names from caller to function and back again.


The Complete Object Flow - The Inbound Journey (train(model)): The caller has a name (model) pointing to a heap object. When calling the function, the caller hands that 8-byte pointer to the function. Python spawns a new execution frame, creates a local variable name, and points it to that exact same object. The data object remains entirely stationary on the heap.

The Outbound Journey (model = load_model()): The function instantiates or grabs a heap object and points a local name to it. When returning, it drops its local frame name but passes that same 8-byte pointer back to the caller. The caller immediately catches the pointer and registers it under a name (model) in its own namespace.

In both directions, the heavy data objects never move, never change position, and are never copied. Only the tiny 8-byte tracking pointers are handed back and forth across execution frames.