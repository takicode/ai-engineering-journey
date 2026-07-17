# Lesson 3 — Global Scope

The Question

Imagine this program:

x = 100

def add():
    y = 50

Everybody says

"x is global."

But...

Where exactly is this "global" variable?

Inside RAM?

Inside the stack?

Inside the heap?

Inside the function?

Inside Python?

Where?

Most programmers have never asked this.

By the end of this lesson you'll know exactly where it lives.

Let's Remember the Mental Model

When Python starts running a program, it creates several things.

One of them is a namespace.

We already learned that a namespace is essentially

a mapping between names and objects.

Conceptually:

    name
    ↓
    object

    Example

    x
    ↓
    10

Notice something.

The namespace doesn't contain the integer.

It only contains the binding.

The integer still lives elsewhere.

Where Does the Integer Live?

Exactly where we've always said.

    Heap

    +-------------+
    | Integer 10  |
    +-------------+

The namespace merely stores

    "x"

    ↓

    (address of Integer 10)

Before Any Function Runs

Suppose our program is

    language = "Python"

    year = 1991

Conceptually

Global Namespace

    language -----------+
                        |
    year ---------------+
                        |
                        ▼

                        Heap

                        "Python"

                        1991

Notice something.

There are no local namespaces yet.

Only one namespace exists.

The global namespace.

## Why Is It Called "Global"?

Because every function can look up names there.

Notice the wording.

Not necessarily modify them.

Just look them up.

That distinction is incredibly important.

We'll return to it later.

## What Happens When a Function Runs?

language = "Python"

    def hello():

        print(language)

Python creates another namespace.

Global Namespace

    language ------+

    hello ---------+

                   |

                   ▼

                  Heap

                 "Python"

Function hello

When we call

hello()

Python creates

Local Namespace

(empty)

because the function has no local variables.

Now two namespaces exist simultaneously.

Name Lookup

Inside

print(language)

Python asks

Do I have a local variable called language?

No.

So it looks elsewhere.

Where?

The global namespace.

There it finds

    language

    ↓

    "Python"

Problem solved.

Notice something.

The function did NOT receive a copy.

The function did NOT duplicate memory.

It simply performed a lookup.

This is one reason Python is memory-efficient.

Think Like an Operating System

Imagine a large office building.

Every employee has

their own desk.

That's local scope.

The company also has

a central document archive.

That's the global namespace.

When Alice needs the employee handbook,

she doesn't copy the handbook onto her desk.

She walks to the archive,

reads it,

and comes back.

Functions behave similarly.

Why Doesn't Python Copy Globals?

Imagine this.

Large AI Model

40 GB

Suppose Python copied globals every time a function executed.

    train()

      ↓

    40 GB copy

    evaluate()

       ↓

    40 GB copy

    save()

       ↓

    40 GB copy

    Memory would explode.

Instead,

all functions simply reference the same object.

## Important Distinction

Global does not mean

stored everywhere.

Global means

stored in the program's global namespace.

The object still lives on the heap.

Only the name lives in the namespace.

This distinction is one of the foundations of Python's object model.

## A Common Misconception

People often think this:

    Global Variable

    ↓

    Memory

Not quite.

It's really

    Global Namespace

    ↓

    Name

    ↓

    Object

    ↓

    Heap

The variable is never the object.

The variable is just the binding.

Exactly the same rule we've been using since Chapter 2.

Nothing changed.

We're simply introducing another namespace.

## Why Large Projects Avoid Globals

Imagine an AI application with:

preprocessing
training
evaluation
checkpointing
monitoring
inference

Now imagine every function freely changing global variables.

Soon you'd have questions like:

Who changed learning_rate?
Why did model suddenly become None?
Which function modified config?
Why did inference stop working after evaluation?

The larger the system becomes, the harder these questions are to answer.

That's why experienced engineers try to minimize mutable global state.

It's not because globals are "bad." It's because shared mutable state makes systems harder to reason about, test, and maintain.

Mental Model

Keep this picture in your head:

               GLOBAL NAMESPACE

        config -----------+
        model ------------+
        train ------------+
                           |
                           |
                           ▼

                     Heap Objects

                Config Object
                Model Object
                Function Object


        ↓ call train()


             LOCAL NAMESPACE

        batch
        loss
        optimizer

The local namespace belongs to one function call.

The global namespace belongs to the module (the Python file that's being executed).

Both namespaces contain names, not the objects themselves.

## AI Engineering Insight

Many modern AI frameworks deliberately reduce reliance on global variables.

Instead of this:

train() magically reads a global model

they prefer:

train(model)

or

Trainer(model)

Why?

Because making dependencies explicit leads to code that's easier to understand, test, reuse, and scale. As we progress into functions, modules, and system design, you'll see this principle appear again and again.

