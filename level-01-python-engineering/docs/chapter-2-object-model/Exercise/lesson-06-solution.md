# Exercises
## Exercise 1

In your own words:

Why isn't reference counting alone enough for Python?

Reference counting only works if an object's lifespan has a clear, linear beginning and end. If two objects point to each other in a loop, their counters will never drop to zero, even if the rest of your program completely forgets about them. This causes memory leaks

## Exercise 2

Consider:

    class Node:
        pass

    a = Node()
    b = Node()

    a.next = b
    b.next = a

    a = None
    b = None

Conceptually explain:

Why don't the objects disappear immediately?
Why are they actually considered garbage?

Why don't the objects disappear immediately? a points to b, and b points to a. Because they form a mutual loop, both objects have a reference count of at least 1. Reference counting only deletes an object when its count hits 0.

Why are they considered garbage? When a = None and b = None happen, the program destroys its direct ties (or handles) to a and b. You can no longer reach or use either object in the program, even though they remember each other.

## Exercise 3

Explain the difference between:

Reference count = 0
Unreachable object

Can an unreachable object have a reference count greater than zero?

Why?

Reference count = 0: The object is no longer being pointed to by any variable, property, or list. Python immediately deletes it.

Unreachable object: The object might have a reference count greater than zero, but it is completely cut off from the main executing program.

Can an unreachable object have a count >0? Yes, as shown in Exercise 2. If object X and object Y reference each other, they will always have a count of at least 1, even if the program has no way to access them.

## Exercise 4

Imagine a program creates thousands of circular references every second.

What would happen if Python had:

reference counting only,
but no garbage collector?

Think about a web server running continuously for months.

If Python relied only on reference counting, those thousands of circular loops created every second would never be deleted. Because the server runs continuously for months, these lost-in-memory objects would pile up. Eventually, the server would consume all available RAM and crash. The cyclic garbage collector prevents this by periodically scanning for and destroying these hidden loops

## Exercise 5 (Thinking)

Suppose Python removed reference counting entirely and relied only on garbage collection.

Name at least four disadvantages this would introduce regarding:

memory usage,
performance,
responsiveness,
temporary objects.

Higher Memory Usage: Objects wouldn't be freed instantly when their local variables expire. They would sit in memory until the garbage collector runs, requiring more overall RAM.

Poor Responsiveness (Lag Spikes): Instead of a smooth teardown object-by-object, the system must occasionally "stop the world" to perform a heavy, full-heap trace. This causes noticeable pauses.

Slower Deallocation: With reference counting, deallocating an object is practically free. Searching through memory objects to see if they are referenced takes much longer.

Wasted CPU on Temporary Objects: Short-lived objects used in math or loops would survive until the next major garbage collection pass, wasting processor cycles that could have been used for immediate cleanup

## Exercise 6 (Challenge)

A developer says:

"If an object's reference count is greater than zero, then the object must still be useful."

Write a response correcting this statement.

Explain the difference between having references and being reachable by a running program.

Correction: An object's reference count can easily be greater than zero, even if it is completely useless to the program. Circular references (Exercise 2) are the classic example of this.

References vs. Reachability: A "reference" simply means an object is being pointed to by another object or variable in memory. Being "reachable" means that the object can be accessed by the main running program starting from a live local variable, global variable, or active stack frame. An object having references doesn't matter if those references are in an isolated island of memory completely cut off from the main code