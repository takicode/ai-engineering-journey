## Lesson 10 — Scope Internals
The Big Question

We've been using the word namespace for several lessons.

But...

What actually is a namespace?

Is it some magical place?

A hidden memory region?

A special Python feature?

No.

A namespace is simply a mapping between names and objects.

Conceptually:

    "x"  ─────► 10

    "name" ───► "Alice"

    "numbers" ─► List Object

    "train" ───► Function Object

Python just needs a way to answer questions like:

"When someone says numbers, which object do they mean?"

### Think Like a Phone Book

Imagine a phone book.

    Alice  →  555-1234

    Bob    →  555-6789

    John   →  555-9999

The phone book doesn't contain people.

It contains:

    name

      ↓

    information

A namespace is exactly the same.

    name

      ↓

    object reference

Notice something.

It doesn't contain the object.

Only the reference.

### Local Namespace

Suppose:

    def work():
        x = 10
        y = []

Conceptually:

Local Namespace

    "x" ─────► Integer Object

    "y" ─────► List Object

The integer lives on the heap.

The list lives on the heap.

The namespace only remembers where they are.

Global Namespace

Now:

    x = 100

    message = "Hello"

Conceptually:

Global Namespace

    "x" ─────────► Integer

    "message" ──► String

Same idea.

Different namespace.

## Function Call

Now let's combine everything we've learned.

Suppose:

    x = 100

    def calculate():

        y = 50

Before calling:

Global Namespace

    x

    calculate

Call:

    calculate()

Python creates something new.

## Execution Frame

Every function call creates an execution frame.

An execution frame contains:

local namespace
bookkeeping information
current line number
links to other frames

Conceptually:

    Execution Frame

    ↓

    Local Namespace

    ↓

    Names

This frame exists only while the function runs.

## Call Stack

Suppose:

    main()

      ↓

    train()

      ↓

    forward()

      ↓

    matmul()

Python creates frames.

Stack Top

    matmul()

    ↓

    forward()

    ↓

    train()

    ↓

    main()

This is the call stack.

Each frame has:

its own namespace
its own local variables
its own execution state

When a function returns:

The top frame disappears.

Exactly like we discussed during variable lifetime.

### Connecting Everything

Let's revisit something from Chapter 2.

    numbers = [1,2,3]

We now know:

      Frame

        ↓

    Namespace

        ↓

    "numbers"

        ↓

    List Object

        ↓

       Heap

Nothing is stored "inside the variable."

The variable is simply a name in a namespace.

## Why Local Variables Are Faster

Interesting question.

Why is:

    x

inside a function usually faster than

    global_x

Because Python already has the current frame.

Conceptually:

    Current Frame

        ↓

    Local Namespace

        ↓

    Found immediately

Globals require another lookup.

    Current Frame

         ↓

    Global Namespace

         ↓

    Found later

The difference is tiny.

But in code executed billions of times (AI loops, numerical computing, interpreters), tiny differences matter.

This is one reason Python optimizes local variable access.

## Frames Are Independent

Imagine:

    def square():

called 10,000 times.

Do they share one frame?

No.

Each call gets a completely new execution frame.

Like hotel rooms.

    Call 1

      ↓

    Frame A

    ----------------

    Call 2

      ↓

    Frame B

    ----------------

    Call 3

      ↓

    Frame C

The rooms may look identical.

But they're separate.

## Why Recursion Works

Consider:

factorial(5)

calls

factorial(4)

calls

factorial(3)

...

If Python reused one frame...

every recursive call would overwrite the previous one.

Impossible.

Instead:

    factorial(1)

        ↓

    factorial(2)

        ↓

    factorial(3)

        ↓

    factorial(4)

        ↓

    factorial(5)

Each has its own frame.

That's why recursion works.

## AI Engineering Example

Suppose an inference server handles:

    Request A

    Request B

    Request C

Each request calls:

    predict()

Each request gets:

    Frame A

    Frame B

    Frame C

The local variables never interfere.

Imagine if all requests shared one frame.

Disaster.

Request A could overwrite Request B's inputs halfway through inference.

Frame isolation is fundamental to concurrent software.

### The Mental Model We've Built

Let's connect Chapters 2 and 3.

When Python executes:

    x = [1,2,3]

Mentally picture:

     Execution Frame
            │
            ▼
        Namespace
            │
            ▼
        Name ("x")
            │
            ▼
        Reference
            │
            ▼
        List Object
            │
            ▼
        Heap Memory

That single diagram explains almost everything we've studied:

assignment
references
identity
mutability
rebinding
garbage collection
namespaces
scope
closures
variable lifetime

They're all different views of the same underlying system.

