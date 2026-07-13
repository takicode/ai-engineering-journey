# Why Computers Use Binary

Computers are made of billions of tiny electronic switches called:

Transistors

A transistor can be:

OFF
ON

or approximately:

0 volts
5 volts

Two states.

Perfect for:

0 and 1
Why Not Decimal?

Imagine trying to build electronics that distinguish:

    0V
    0.5V
    1V
    1.5V
    2V
    ...
    5V

Tiny electrical noise could cause mistakes.

Binary gives us:

    Low
    High

which is much more reliable.

The Big Idea

Binary isn't magic.

It's simply:

A numbering system with base 2.

Just like decimal is:

Base 10
Decimal System (Base 10)

Digits:

    0 1 2 3 4 5 6 7 8 9

Places:

    1
    10
    100
    1000
    ...

Example:

    352

means:

    3 × 100
    +
    5 × 10
    +
    2 × 1
    =
    352
Binary System (Base 2)

Digits:

    0 and 1

Places:

    1
    2
    4
    8
    16
    32
    64
    ...

which are:

    2⁰
    2¹
    2²
    2³
    2⁴
    ...

Example 1

Binary:

1

Decimal:

1

Example 2

Binary:

    10

    Decimal:

    2

because:

    1 × 2¹ + 0 × 2⁰
    =
    2
Example 3

Binary:

101

Decimal:

1 × 4
+
0 × 2
+
1 × 1
=
5
Example 4

    Binary:

    1101

    Decimal:

    1×8 + 1×4 + 0×2 + 1×1
    =
    13

    Visual Method
    8   4   2   1
    1   1   0   1

Result:

    8 + 4 + 1 = 13

## Decimal to Binary

Example:

Convert:

13

to binary.

Repeated division:

    13 ÷ 2 = 6 remainder 1
    6 ÷ 2 = 3 remainder 0
    3 ÷ 2 = 1 remainder 1
    1 ÷ 2 = 0 remainder 1

Read upward:

## 1101

## Why This Matters

Everything becomes binary:

Text
Images
Audio
Videos
Python files
AI models

Everything.

Example

This:

x = 5

is stored as bytes.

Bytes are stored as bits.

Bits are:

0s and 1s.
AI Connection

Suppose an LLM has:

70 billion parameters

Each parameter is stored as bits.

A huge amount of AI engineering is simply:

How do we store and move all these bits efficiently?

Mental Model
Everything
↓
Bytes
↓
Bits
↓
0 and 1
