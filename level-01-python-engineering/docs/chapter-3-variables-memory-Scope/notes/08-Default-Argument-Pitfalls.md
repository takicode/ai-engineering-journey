Lesson 8 — Default Argument Pitfalls
A Question

Suppose I write:

def add_item(item, items=[]):
    items.append(item)
    return items

Most beginners think this means:

"Every time I call the function, Python creates a fresh empty list."

That seems reasonable.

But it is wrong.

Why?

To answer that, we need to think about when functions are created.

Not when they are called.

Building the Mental Model

Imagine Python reading your file.

def greet():
    print("Hello")

When Python reaches this line, it doesn't just memorize some text.

It creates a function object.

Remember Chapter 2?

Everything is an object.

So somewhere on the heap:

Heap

+---------------------------+
| Function Object           |
|                           |
| name: greet               |
| code: ...                 |
| defaults: ???             |
+---------------------------+

That function object lives until nothing references it.

Now Add a Default Value
def add_item(item, items=[]):
    items.append(item)
    return items

What happens?

Python first creates the empty list.

[]

Then it creates the function object.

Then it stores a reference to that list inside the function object itself.

Conceptually:

Global Namespace

add_item
    |
    |
    ▼

+------------------------------+
| Function Object              |
|                              |
| code                          |
| defaults -------------------+
+------------------------------+
                               |
                               ▼
                          +----------+
                          |   []     |
                          +----------+

Notice something important.

The list already exists.

It is not waiting to be created later.

Then the Function is Called

Suppose:

add_item("apple")

Python asks:

"Did the caller provide items?"

No.

So it uses the stored default.

Not a new one.

The existing one.

The list becomes

["apple"]

Second call:

add_item("banana")

Again Python asks:

Did the caller pass items?

No.

Use the stored default.

Which is now

["apple"]

Append again.

["apple", "banana"]

Nothing mysterious happened.

The function kept using the same object.

The Important Insight

Many people think:

Call Function

↓

Create default value

↓

Run

Reality:

Define Function

↓

Create default object

↓

Store inside function object

↓

Call Function

↓

Reuse stored object

That is the entire reason this "bug" exists.

It isn't a bug.

It is a consequence of how Python builds function objects.

Why Did Python Choose This Design?

Imagine default values were recreated every call.

def connect(timeout=30):
    ...

Every function call would need to recreate

30

Then:

def connect(name="localhost"):

Recreate the string.

Every call.

Every function.

For millions of function calls.

Python instead says:

"I'll build the defaults once."

This is faster.

It works perfectly for immutable objects.

30

"localhost"

True

None

False

Because they cannot change.

So Why Are Mutable Objects Different?

Suppose the default is

[]

Lists can mutate.

The object stored inside the function changes.

The function keeps pointing to the same object.

So every later call observes the mutation.

Exactly like this:

Function Object

        |
        |
        ▼

+------------------+
| []               |
+------------------+

↓

append("A")

↓

+------------------+
| ["A"]            |
+------------------+

↓

append("B")

↓

+------------------+
| ["A","B"]        |
+------------------+

Nothing new was created.

The same object changed.

This Connects Everything We've Learned

Think about every lesson.

Object Model

Objects live on the heap.

✓

References

Functions store references.

✓

Mutability

Lists mutate.

✓

Lifetime

The list survives because the function object references it.

✓

Namespaces

The default isn't in the local namespace.

It belongs to the function object.

✓

Suddenly this famous Python behavior becomes completely logical.

The Correct Pattern

Instead of:

def add_item(item, items=[]):
    ...

Use:

def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)

    return items

Now think through the execution.

Each call that doesn't supply items does:

items = None

↓

Create NEW list

↓

Use it

↓

Function ends

↓

List dies (unless returned or referenced elsewhere)

Every call gets a fresh object.

Why AI Engineers Should Care

Imagine:

def preprocess(batch=[]):

Thousands of training batches pass through.

If that list is reused accidentally:

samples from previous batches leak into future batches
preprocessing becomes nondeterministic
experiments become impossible to reproduce
debugging becomes extremely difficult

In production ML systems, these kinds of bugs are among the hardest to track down because nothing crashes—the state simply "sticks" across calls.

Understanding why this happens helps you avoid subtle bugs instead of memorizing a rule.

Mental Model to Remember

Whenever you see:

def f(x=[]):

Don't think:

"Python creates an empty list every call."

Think:

"Python created one list when it created the function object. Unless I pass another argument, every call reuses that same list."

That single idea explains the entire behavior.

