# Lesson 2 — Defining vs Calling a Function

This lesson is short but extremely important.

One of the biggest misconceptions beginners have is thinking that writing a function means running a function.

Python treats those as two completely different events.

Think of a Restaurant

Imagine a restaurant.

Writing the recipe isn't cooking.

The recipe simply tells the chef how to cook later.

      Recipe
        │
        ▼
    Stored in cookbook

(No food exists yet.)

Only when a customer orders it does the chef actually start cooking.

    Customer orders

          ↓

    Chef starts cooking

         ↓

    Food is produced

Functions work exactly the same way.

## Defining

When Python reaches

    def greet():
        print("Hello")

Python does not execute

    print("Hello")

Instead it says

"I'm creating a function object that knows how to do this later."

Conceptually:

     Source Code

         ↓

    Compile function body

         ↓

    Create Function Object

         ↓

    Bind name "greet"


Execution stops there.

No function frame is created.

No parameters exist.

Nothing inside the body runs.

## Calling

Later you write

greet()

Now something completely different happens.

Python sees

    Function Object

         +

    ()

and says

"Execute the instructions stored inside this object."

Now Python creates a brand-new execution frame.

        greet()

           ↓

        Create Frame

           ↓

        Create Local Namespace

            ↓

        Execute Bytecode

            ↓

        Destroy Frame

            ↓

         Return

Notice something important:

The function object already existed before the frame did.

The frame only exists while the function is running.

## Defining Happens Once

Suppose

    def greet():
        print("Hello")

This executes one time.

Only one function object is created.

    greet

      ↓

    Function Object

Calling it

    greet()
    greet()
    greet()

does not create three function objects.

It creates

One Function Object

Three Execution Frames

This distinction is fundamental.

The Timeline

Imagine this code

    print("A")

    def greet():
        print("Hello")

    print("B")

    greet()

    print("C")

Conceptually Python walks through the file.

        Start

          ↓

        print("A")

          ↓

        Output:
          A

          ↓

        Reach def

          ↓

        Create Function Object

          ↓

        Continue

          ↓

        print("B")

          ↓

        Output:
           B

          ↓

        Reach greet()

          ↓

        Create Frame

          ↓

        Run body

          ↓

        Output:
        Hello

          ↓

        Destroy Frame

          ↓

        Continue

          ↓

        print("C")

          ↓

        Output:
          C

Notice that Python never "jumps into" the function when it first sees def.

It simply stores it for future use.

Another Mental Model

Imagine a DVD.

    Movie

    ↓

    Stored on DVD

Owning the DVD doesn't mean the movie is playing.

Only pressing Play starts the movie.

Similarly

Function Object

≠

Running Function

Calling the function is pressing Play.

## AI Engineering Connection

Almost every AI library depends on this distinction.

When you write

optimizer.step

you are referring to a function object.

When the framework later does

optimizer.step()

it executes it.

The same applies to:

PyTorch callbacks
FastAPI endpoints
Flask routes
TensorFlow training loops
schedulers
event handlers

Frameworks constantly pass around function objects and decide when to call them.

If you don't distinguish definition from execution, many advanced Python patterns feel like magic.

## Mental Model
        def greet():
            ...

        ↓

        Create Function Object

        ↓

        Bind name

        ↓

        (wait...)

        ↓

        greet()

        ↓

        Create Frame

        ↓

        Execute Code

        ↓

        Destroy Frame

        ↓

        Return
