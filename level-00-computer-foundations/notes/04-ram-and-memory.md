# RAM and Memory

Layer 1: Intuition

Imagine you're cooking.

You have:

a warehouse (SSD)
a kitchen counter (RAM)
your hands (registers)

The workflow:

        Warehouse (SSD)
             ↓
        Kitchen Counter (RAM)
             ↓
        Hands (Registers)
             ↓
        Cooking (CPU)

Would you go to the warehouse every time you need salt?

No.

You bring ingredients to the counter first.

RAM is that counter.

## What is RAM?

RAM stands for:

Random Access Memory

It is:

temporary
fast
volatile
directly accessible by the CPU

Its job is to hold:

running programs,
variables,
temporary data,
program state.

## Why Is It Called "Random Access"?

This is one of those names that confuses beginners.

"Random" does not mean:

unpredictable

It means:

Every memory location can be accessed in approximately the same amount of time.

Imagine lockers:

Locker 1
Locker 2
Locker 1000
Locker 1,000,000

You can open any locker directly.

That's random access.

Contrast With Tape Storage

Old magnetic tapes worked like this:

        Start
        ↓
        1
        ↓
        2
        ↓
        3
        ↓
        4
        ↓
        ...

To get to position 1000:

you had to pass through 999 positions first.

That's called:

Sequential Access

RAM is much faster because it supports direct access.

Memory Is Just a Huge Collection of Boxes

Imagine memory like this:

        +-----+
        |     |
        +-----+
        |     |
        +-----+
        |     |
        +-----+
        |     |
        +-----+

Each box:

stores data,
has an address.
Memory Addresses

Every location in RAM has an address.

Example:

Address      Value
1000         5
1001         10
1002         20

The CPU uses addresses to find data.

Why Addresses Matter

Suppose:

x = 10

The computer might do:

Address 5000
↓
10

Then:

y = 20
Address 5001
↓
20

The exact addresses change every time you run the program.

Important Idea

Variables are not the data itself.

Variables are names that help us reach data stored somewhere in memory.

This idea becomes extremely important in Python.

Why RAM Is Volatile

==> RAM needs electricity to maintain its state.

Power off:

RAM → empty

That's why:

x = 5

disappears after shutdown.

What Lives in RAM?

When you open:

Chrome,
VS Code,
Python,

all of them are loaded into RAM.

Your operating system also lives in RAM while it's running.

Example

You run:

numbers = [1, 2, 3]

Some memory is allocated.

Simplified:

Address      Value
5000         1
5001         2
5002         3

Reality is more complicated, but this model is good enough for now.

Why AI Engineers Care About Memory

Suppose:

model = HugeLLM()

The model weights may require:

20 GB
40 GB
80 GB

If you don't have enough memory:

Out of Memory Error

Understanding memory is essential.

## Stack vs Heap (Introduction)

We'll study this deeply later.

For now:

Stack

Usually stores:

function calls,
local information,
execution context.


Heap
Usually stores:

dynamically allocated objects,
large data structures.

For now, remember:

Stack → function management
Heap → object storage


Mental Model
    SSD
    ↓
    RAM
    ↓
    Registers
    ↓
    CPU

This model should now feel natural.

A Question for You

Suppose:

x = 5
y = x

Do you think:

two copies of 5 are created in memory?

or

both variables somehow refer to the same thing?

Don't worry about being right.

I want your intuition.

This question will become one of the biggest ideas in Python:

Objects
References
Identity
Mutability
Repository Work



## Important Insight

Variables are names that refer to objects in memory.

Multiple variables can refer to the same object.

Example:

x = 5
y = x

Both x and y refer to the same integer object.
