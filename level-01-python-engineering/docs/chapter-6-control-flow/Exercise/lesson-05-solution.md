
Exercises
Exercise 1 — Mental Model

In your own words:

What actually changes on each iteration of a for loop?

Does Python create a new loop variable every iteration?

Why is rebinding different from mutation?

Exercise 2 — Predict the Output

Without running the code, determine the output and explain why.

numbers = [10, 20, 30]

for number in numbers:
    print(number)

print(number)
numbers = [1, 2, 3]

for number in numbers:
    number = 100

print(numbers)
matrix = [
    [1],
    [2]
]

for row in matrix:
    row.append(99)

print(matrix)
Exercise 3 — Write Code

Write a program that:

Creates a list of five AI model names.
Uses a for loop to print:
Loading model: <model_name>

For each model.

Then create a second program that stores a list of scores:

scores = [91, 85, 78, 99, 88]

Use a for loop to print:

Excellent

for scores 90 and above, otherwise print:

Keep Improving
Exercise 4 — AI Engineering Thinking

Suppose you have:

batches = [batch1, batch2, batch3]

A junior engineer says:

"Python duplicates every batch during the for loop."

Evaluate this statement.

Explain:

What actually happens on each iteration.
What the loop variable refers to.
Why Python was designed this way.
Why copying every batch would be disastrous for large AI datasets and GPU training.