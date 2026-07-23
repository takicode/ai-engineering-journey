

Exercises
Exercise 1 — What is a Boolean?

In your own words:

What is a Boolean?
Is True a keyword, an object, or both?
Why is bool considered a type?
Exercise 2 — Following the Evaluation

Without running code, explain what conceptually happens when Python evaluates:

score = 92

score >= 90

Describe the timeline from looking up score to producing the final result.

Exercise 3 — Identity vs Equality

Suppose:

a = [1, 2]

b = [1, 2]

Explain:

Why a == b evaluates differently from a is b.
Which comparison asks about values?
Which comparison asks about object identity?
Why both comparisons return Boolean objects.
Exercise 4 — AI Engineering Thinking

Imagine you're building an AI fraud detection system.

One rule says:

Transaction amount is below the daily limit.
User authentication succeeded.
Card is not blocked.

Explain why these are naturally represented as Boolean values rather than numbers or strings.

Then explain how combining them with and, or, and not allows the system to make decisions.

In the next lesson, we'll learn one of the most elegant ideas in Python:

Truthiness.

You'll discover why objects like empty lists, empty strings, and None can be used directly in if statements—even though they aren't Boolean objects. This concept is used constantly in professional Python code.