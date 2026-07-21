# Chapter 4 — Functions
## Lesson 1 — What is a Function Object?

Question:

What actually is a function?

Most programmers answer:

"A function is a reusable block of code."

That isn't wrong.

But it's also not how Python thinks.

Remember one of the biggest ideas from Chapter 2?

Everything is an object.

That includes functions.

A function is not a special language feature.

A function is an object.

That single statement explains almost every "advanced" feature in Python.

Let's write our first code of this chapter.
    def greet():
        print("Hello")

Most beginners think Python stores something like this:

    greet
     ↓
    code

But that's not what happens.

Python creates a Function Object.

Conceptually:

    Global Namespace

    greet
    │
    ▼
    +----------------------+
    | Function Object      |
    |----------------------|
    | name = "greet"       |
    | parameters = ()      |
    | code = ...           |
    | defaults = ...       |
    | globals = ...        |
    | closure = ...        |
    +----------------------+

Notice something.

The name greet is not the function.

Exactly like:

    x = [1,2,3]

doesn't make x the list.

Likewise,

    def greet():
        ...

doesn't make greet the function.

The function is an object on the heap.

greet is merely a name bound to that object.

Exactly the same model you've already learned.

This should feel familiar.

Earlier we learned

    x = 5

means

    x
    │
    ▼
    Integer Object

Now we simply replace the integer.

    greet
    │
    ▼
    Function Object

Nothing new.

Just a different object type.

So what does def actually do?

Many people think def means

"Create a function."

Not exactly.

Conceptually it does three things.

### Step 1

Python builds a Function Object.

    Heap

    +----------------------+
    | Function Object      |
    +----------------------+

### Step 2

It stores all the information needed to execute later.

parameter list
bytecode
default arguments
annotations
module
globals reference
closure information

Notice something important.

The function body does not run.

It is merely packaged.

Think of sealing instructions inside a box.

### Step 3

Python binds the name.

Global Namespace

    greet
    │
    ▼
    Function Object

Sound familiar?

It's literally assignment.

Conceptually,

    def greet():
        ...

behaves like

greet = <Function Object>

Not identical internally, but that's the correct mental model.

Calling the function

Now:

    greet()

What happens?

Not:

"Python jumps into the function."

That's too vague.

Using Chapters 2 and 3:

    Execution Frame

          ↓

    Look up name "greet"

          ↓

    Find Function Object

          ↓

    Create NEW execution frame

          ↓

    Bind parameters

          ↓

    Execute bytecode

          ↓

    Destroy frame

          ↓

       Return

Notice how many previous chapters were required just to explain one function call.

That's why we delayed writing code.

Now every piece has somewhere to fit.

## The biggest misconception

People often believe

def greet():

is the function.

It isn't.

It's an instruction that creates the function object.

Exactly like

    []

creates a list object.

or

    {}

creates a dictionary object.

or

    5

creates (or reuses) an integer object.

Everything follows the same object model.

## Why this matters for AI Engineering

Frameworks like:

PyTorch
FastAPI
LangChain
Hugging Face Transformers
TensorFlow

all rely on one fact:

Functions are ordinary objects.

That's why you can do things like:

pass a function into another function
return a function
wrap a function
register callbacks
build decorators
create training loops
define custom loss functions
implement optimizers

None of these are "special features."

They're consequences of the fact that a function is just another Python object.

## Mental Model

Instead of remembering:

"Functions are reusable blocks of code."

Upgrade your model to:

A function is a Python object that stores executable code and the information needed to execute that code later.

The name is separate from the function.

Calling the function creates an execution frame, executes the stored code, then destroys the frame while the function object itself continues to exist.

This is a much more accurate mental model, and it will make advanced topics like decorators and callbacks feel natural instead of magical.

