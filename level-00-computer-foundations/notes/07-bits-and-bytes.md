## Intuition

Let's start with a question.

Suppose I ask you to answer:

Is the light ON?

You can only answer:

Yes
No

That's exactly one bit of information.

A bit (Binary Digit) is the smallest unit of information a computer can represent.

It answers a question with two possible outcomes.

Examples:

Is the door open?
0 = No
1 = Yes
Is the user authenticated?
0 = No
1 = Yes
Is the payment successful?
0 = Failed
1 = Success

Notice something.

A bit doesn't have a fixed meaning.

A bit is just a container.

We give it meaning based on context.

This idea will become incredibly important later when we discuss tensors and embeddings.

Layer 2 — One Bit Isn't Enough

Suppose I ask:

Which day is today?

Can one bit answer that?

No.

One bit only has:

0
1

Two possibilities.

But the days of the week have:

Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday

Seven possibilities.

One bit isn't enough.

Layer 3 — Add More Bits

Suppose we have 2 bits.

Possible values:

00
01
10
11

How many possibilities?

Let's count.

00
01
10
11

That's 4.

Notice the pattern.

Bits	Possible Values
1	2
2	4
3	8
4	16
5	32
6	64
7	128
8	256

Do you see the pattern?

Every extra bit doubles the number of possible combinations.

Mathematically:

Number of combinations = 2ⁿ

where n is the number of bits.

Stop and Think

Why?

Imagine you already have:

00
01
10
11

Now you add one more bit in front.

Each existing combination can now start with:

0

or

1

So the number of combinations doubles.

This isn't magic.

It's simple combinatorics.

Layer 4 — Why 8 Bits?

Here's a question.

If 7 bits already give us:

128 values

Why didn't engineers stop there?

Why not:

7-bit computers?

Or:

9-bit computers?

Historically, early computers actually did use different word sizes.

Some used:

6 bits
7 bits
9 bits
12 bits
36 bits

There was no universal standard.

Over time, 8 bits became the sweet spot because:

256 possible values were enough for characters and control codes.
It's easy to divide into larger units (16, 32, 64 bits).
Hardware design became standardized.

So:

8 bits = 1 byte

is a convention, not a law of nature.

Layer 5 — What Can One Byte Represent?

One byte has:

8 bits

Possible values:

2⁸ = 256

So one byte can represent:

0
to
255

Exactly 256 different values.

Example

Binary:

00000000

Decimal:

0

Binary:

00000001

Decimal:

1

Binary:

11111111

Decimal:

255
Where Do Letters Come From?

Suppose I write:

A

The CPU doesn't understand the shape "A".

Instead, we agree on a mapping.

For example (ASCII):

A → 65

Then:

65

becomes binary:

01000001

So when you type:

print("A")

The computer is ultimately working with:

01000001

Later we'll learn about Unicode, which lets computers represent characters from virtually every language.

## AI Connection

Imagine an AI model stores one parameter as a 32-bit floating-point number.

If the model has:

1 billion parameters

Then just the parameters require roughly:

1,000,000,000 × 4 bytes
≈ 4 GB

This is why understanding bits and bytes matters.

Memory usage in AI is often calculated in bytes.

Mental Model
Bit
↓
Smallest unit (0 or 1)

8 Bits
↓
1 Byte

Bytes
↓
Represent numbers, text, images, audio...

Everything becomes bytes.
Common Beginner Mistake

People say:

"A character is always one byte."

That's not true.

It depends on the encoding.

For example:

A

may use one byte in ASCII or UTF-8.

But:

😊

uses multiple bytes in UTF-8.

We'll cover encodings later, so don't worry about the details yet.


## Key Insights

- A bit is the smallest unit of information and can represent one of two states.
- Adding one more bit doubles the number of possible combinations.
- A byte is 8 bits and can represent 256 different values.
- Computers store numbers, text, images, and programs as sequences of bytes.


## Insights Beyond the Lesson

### Information Grows Exponentially

Every additional bit doubles the number of possible combinations.

This means that a small increase in the number of bits can represent dramatically more information.

Examples:

- 8 bits = 256 values
- 16 bits = 65,536 values
- 32 bits = 4,294,967,296 values

This exponential growth is one of the fundamental ideas behind computing.