Exercises
Exercise 1 — Understanding the Hierarchy

In your own words:

Why does True + True equal 2?
Is bool completely separate from int?
Why did Python design it this way instead of making bool an unrelated numeric type?
Exercise 2 — Following the Types

Without running the code:

x = True

y = x + 5

Conceptually answer:

What type is x?
Why can Python perform the addition?
What type will y reference?
Does True stop being a boolean?
Exercise 3 — Numeric Promotion

Consider:

a = 10

b = 2.5

c = a + b

Without running it:

Why doesn't Python keep the result as an integer?
Which object is promoted conceptually?
Why is promoting upward safer than promoting downward?
Exercise 4 — AI Engineering Thinking

Imagine you're evaluating one million predictions.

Each comparison:

prediction == label

produces a boolean.

Explain:

Why can functions like sum() work naturally with these values?
Why is this useful for computing metrics such as accuracy?
Why is Python's numeric hierarchy a good fit for data science and machine learning?