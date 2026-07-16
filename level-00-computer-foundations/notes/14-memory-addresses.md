# Lesson 14

## Memory Addresses

Imagine your computer has:

16 GB RAM

That's billions of bytes.

Now imagine the CPU wants to read the value 10.

How does it find it?

Does it search the entire RAM?

Of course not.

That would be incredibly slow.

Instead, every location in RAM has an address.

Just like every house on a street has a house number.

Think About Your City

Suppose someone says:

"Deliver this package to John."

Question:

Where?

There could be thousands of people named John.

Now suppose they say:

House 42
Oak Street

Now the delivery person knows exactly where to go.

RAM works the same way.

RAM Is Like a Giant Neighborhood

Imagine RAM as millions (actually billions) of tiny storage boxes.

        +-------+
        |       |
        +-------+

        +-------+
        |       |
        +-------+

        +-------+
        |       |
        +-------+

Each storage box has a unique address.

For example:

Address Value
1000    25
1001    18
1002    99
1003    10
1004    42

The address identifies where the data lives.

The value is what is stored there.

Don't confuse the two.

Address vs Value

Suppose:

Address: 1003

Value: 10

These are completely different things.

1003

is not the number ten.

It's the location where ten happens to be stored.

Just like:

Apartment 205

is not the person living there.

It's where they live.

Why Addresses?

Imagine RAM had no addresses.

Suppose it contained:

10

25

18

900

42

100

...

How would the CPU find:

42

Would it search billions of locations every time?

That would make computers unbelievably slow.

Addresses solve this.

The CPU can immediately say:

Read memory location 1004

No searching.

Just go there.

The CPU Doesn't Understand Names

This surprises beginners.

Suppose your code says:

x = 10

The CPU has absolutely no idea what:

x

means.

It only understands addresses.

Conceptually:

    Name

     ↓

    Memory Address

     ↓

    Data

We'll later learn that CPython maintains a mapping from names like x to objects.

The CPU itself never sees the name x.

Memory Is Just Bytes

Remember our earlier lesson.

RAM stores bytes.

Suppose memory looks like this:

Address  Data

1000     01101010

1001     11001001

1002     00101010

1003     10100111

The CPU doesn't see:

Integer

String

List

Dictionary

It sees bytes.

Software gives those bytes meaning.

This idea is fundamental.

Reading Memory

Suppose the CPU needs the value stored at address:

1003

Conceptually it performs:

    Read address 1003

        ↓

    Memory Controller

        ↓

       RAM

        ↓

    Return byte(s)

        ↓

    CPU Register

Notice something.

The value first enters a register.

We learned this weeks ago.

Nothing is wasted.

Every lesson connects.

Writing Memory

Suppose we store:

50

at address:

2000

Conceptually:

    CPU Register

        ↓

    Memory Controller

        ↓

    RAM Address 2000

        ↓

    Store Value

Again:

The CPU never "talks" directly to RAM.

The memory controller coordinates the transfer.

(Modern CPUs have the controller integrated, but this conceptual model is useful.)

One Important Insight

Suppose memory contains:

Address     Value
5000        100

Question:

Can the CPU tell whether:

100

means

an integer?
a character?
part of an image?
part of a neural network?

No.

The bytes themselves don't carry meaning.

Meaning comes from software.

This idea will become incredibly important when we study NumPy and tensors.

Where Does Python Fit?

Suppose we write:

x = 10

Python creates an integer object somewhere in memory.

Imagine:

Address

8000

The object lives there.

Then Python creates the name:

x

which refers to that object.

Conceptually:

        x

        ↓

    Address 8000

        ↓

    Integer Object

        ↓

    Value 10

Notice something.

The name doesn't contain the object.

It refers to where the object is.

This is why we spent so much time on memory addresses before learning Python variables.

Why This Matters

Soon we'll learn:

a = [1, 2, 3]

b = a

Many beginners think:

Copy List

No.

That's not what happens.

Understanding addresses will explain exactly why.

Real Hardware

Do memory addresses really look like:

1000
1001
1002

Not usually.

Modern computers use hexadecimal.

You might see:

0x7FFE81AB32C0

Looks scary.

It's just an address.

Nothing magical.

We'll become comfortable reading them later.

## AI Connection

Imagine a neural network with:

7 billion parameters

Those parameters ultimately live at memory addresses.

When the CPU or GPU performs matrix multiplication, it continuously reads and writes enormous numbers of memory locations.

Efficient memory access is one of the biggest reasons AI systems can be fast—or painfully slow.

Understanding memory isn't just for systems programmers; it's fundamental to high-performance AI.

Common Misconceptions
"Variables are memory."

No.

Variables (or names, in Python) are not memory.

"The CPU knows variable names."

No.

The CPU only knows addresses.

"Addresses store values."

No.

Addresses identify locations.

Locations contain values.

## Mental Model

Think of RAM as a hotel.

Every room has:

a room number (address)
a guest (data)

When someone asks:

"Where is Alice?"

The receptionist doesn't search every room.

They check the room number.

Addresses exist for the same reason.

## Key Insight

Memory addresses identify locations in RAM.

The CPU works with memory addresses, not variable names.

Software gives meaning to the bytes stored at those addresses.