# Lesson 5 — for Loops

Most tutorials teach:

"A for loop repeats code."

That's true.

But it's not what Python is actually doing.

By the end of this lesson you'll understand why Python's for loop is very different from C, Java, or JavaScript.

## The Mental Model

Suppose you have:

    numbers = [10, 20, 30]

What is this?

Not three variables.

Not three loops.

It is one list object containing references to three integer objects.

    numbers
    │
    ▼
    +-----------------------+
    |   List Object         |
    |-----------------------|
    | → 10                  |
    | → 20                  |
    | → 30                  |
    +-----------------------+

The list already exists.

The loop does not create it.

## The First for Loop

    numbers = [10, 20, 30]

    for number in numbers:
        print(number)

Output:

    10
    20
    30

Looks simple.

But let's see what actually happens.

## Step-by-Step Execution

Python reaches

    for number in numbers:

It does not immediately start repeating.

Instead, conceptually:

    Evaluate numbers
    Ask it for something that can produce values one by one
    Receive the first value
    Bind it to number
    Execute the body
    Ask for the next value
    Repeat until there are no more values

Notice something important.

The loop variable is rebound on every iteration.

## Memory View

Initially

    Global Frame

    numbers ─────► List

First iteration

    numbers ─────► List

    number ─────► 10

Second iteration

    numbers ─────► List

    number ─────► 20

Third iteration

    numbers ─────► List

    number ─────► 30

The name number stays the same.

Only its reference changes.

This should remind you of assignment and rebinding from Chapter 2.

### Another Example

    names = ["Alice", "Bob", "Charlie"]

    for name in names:
        print(name)

Timeline

Iteration 1

    name ──► "Alice"

Iteration 2

    name ──► "Bob"

Iteration 3

    name ──► "Charlie"

Again,

Python isn't creating three variables.

It keeps rebinding one local name.

## You Can Use Any Variable Name

These are identical:

    for x in numbers:
        print(x)

    for value in numbers:
        print(value)

    for banana in numbers:
        print(banana)

Python doesn't care.

The name is just a label.

Choose names that make your code readable.

## Looping Over Strings

A string is also something Python can process one character at a time.

    word = "AI"

    for letter in word:
        print(letter)

Output

    A
    I

Notice:

The string object is not split into pieces beforehand.

Python produces one character at a time during the loop.

Looping Over Tuples
    point = (5, 8)

    for value in point:
        print(value)

Output

    5
    8

Exactly the same mental model.

    Nested Loops
    for row in range(2):
        for column in range(3):
            print(row, column)

Conceptually

    Outer Loop

        row = 0

            Inner Loop

            column = 0
            column = 1
            column = 2

        row = 1

            Inner Loop

            column = 0
            column = 1
            column = 2

Each loop has its own loop variable.

## Common Beginner Mistake
    numbers = [1, 2, 3]

    for number in numbers:
        number = 100

    print(numbers)

Many beginners expect

    [100,100,100]

Wrong.

Output

    [1,2,3]

Why?

Because

    number = 100

does not modify the list.

It merely rebinds the local loop variable.

Remember Chapter 2:

Assignment changes names.

Mutation changes objects.

Mutating Instead
    matrix = [
        [1],
        [2],
        [3]
    ]

    for row in matrix:
        row.append(100)

    print(matrix)

Output

    [[1, 100],
    [2, 100],
    [3, 100]]

Why?

Because

row

points directly to each inner list.

Calling

append()

mutates the object.

## A Very Common AI Example

Datasets are processed one sample at a time.

    dataset = [
        "image1.jpg",
        "image2.jpg",
        "image3.jpg"
    ]

    for image in dataset:
        print("Loading", image)

Output

    Loading image1.jpg
    Loading image2.jpg
    Loading image3.jpg

This pattern appears everywhere:

    PyTorch
    TensorFlow
    Hugging Face
    LangChain
    OpenAI SDKs
    
## Training Loop

A simplified training loop might look like:

    dataset = ["batch1", "batch2", "batch3"]

    for batch in dataset:
        print(f"Training on {batch}")

Later, this will evolve into:

    for epoch in range(10):
        for batch in train_loader:
            outputs = model(batch)
            loss = loss_function(outputs)
            optimizer.step()

If you understand for loops deeply, you'll understand the backbone of every deep learning training pipeline.

## Best Practices

✅ Use meaningful variable names.

    for student in students:

instead of

    for x in students:

unless the meaning is genuinely obvious.

Avoid changing the loop variable expecting to modify the original collection.

    item = ...

changes the name.

Not the collection.

When you want to modify objects inside a collection, call methods on the objects themselves (if they're mutable).

