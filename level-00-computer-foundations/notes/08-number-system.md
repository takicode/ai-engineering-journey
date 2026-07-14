# Lesson 8
# Number Systems

Today's goal is not learning three number systems.

Today's goal is understanding that:

The value never changes. Only the representation changes.

This is one of the most important ideas in computing.

Layer 1 — A Number Is Not Its Representation

Let's start with a question.

What is this?

15

You'll probably say:

"Fifteen."

But here's the trick.

That's not the number.

That's one way of writing the number.

Think about language.

The same object can be called:

English: Dog
French: Chien
Spanish: Perro

Different words.

Same animal.

Likewise:

Decimal:     15
Binary:      1111
Hexadecimal: F

Different representations.

Same value.

This distinction is incredibly important.

Analogy

Imagine you have ₦5,000.

You can describe it as:

Five thousand naira
₦5,000
5000

Different representations.

Same amount of money.

## Three Number Systems
Decimal (Base 10)

The one humans naturally use.

Digits:

0 1 2 3 4 5 6 7 8 9

Why?

Probably because we have ten fingers.

Each position represents a power of 10.

Example:

357

means:

    3 × 10²
    +
    5 × 10¹
    +
    7 × 10⁰

Binary (Base 2)

Digits:

0 1

Each position represents:

2⁰
2¹
2²
2³
...

Example:

1011

means:

    8 + 2 + 1
    =
    11

Hexadecimal (Base 16)

Now the interesting one.

Hexadecimal has 16 symbols.

    0 1 2 3 4 5 6 7 8 9
    A B C D E F

Where:

A = 10
B = 11
C = 12
D = 13
E = 14
F = 15

Notice:

We're not inventing new numbers.

We're inventing new symbols.

Why Invent Hexadecimal?

Good question.

Imagine writing:

1111111111111111

How many ones are there?

Hard to count.

Now write the same value in hex.

FFFF

Much easier.

### The Magic Relationship

This is the reason hex became the language of programmers.

Look carefully.

One hex digit:

F

represents:

1111

Exactly 4 bits.

Not approximately.

Exactly.

Examples:

    Binary	Hex
    0000	0
    0001	1
    0010	2
    0011	3
    0100	4
    0101	5
    0110	6
    0111	7
    1000	8
    1001	9
    1010	A
    1011	B
    1100	C
    1101	D
    1110	E
    1111	F

Do you see why programmers love hex?

Instead of writing:

11111111

they write:

FF

Much cleaner.

Why Memory Addresses Are Written in Hex

Suppose memory contains this address:

11111110101011001100000011110000

Would you like debugging with that?

Probably not.

Instead:

0xFEACC0F0

Same value.

Far easier to read.

The 0x prefix simply means:

"The number that follows is hexadecimal."

## AI Connection

When debugging deep learning libraries like PyTorch or TensorFlow, you'll often see:

0x7FFE3A91...

Those are memory addresses.

Today they look mysterious.

By the time we study Python's object model, you'll know exactly what they represent.

One Important Insight

This is where many beginners get confused.

These are all the same value:

Decimal:      26
Binary:       11010
Hexadecimal:  1A

The number did not change.

Only the notation changed.

Think back to our language analogy:

Dog
Perro
Chien

Same animal.

Different languages.

Let's Convert One Together

Convert binary:

10101111

Step 1: Group into 4 bits from the right.

1010 1111

Step 2: Convert each group.

1010 = A
1111 = F

Answer:

AF

No decimal conversion required.


## Key Insight

A number is an abstract quantity.

Binary, decimal, and hexadecimal are simply different ways of representing the same quantity.

Changing the representation does not change the value.