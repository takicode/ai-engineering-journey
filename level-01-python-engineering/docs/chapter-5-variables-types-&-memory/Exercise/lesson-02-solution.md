Exercises
Exercise 1 — Who Has the Type?

In your own words:

Why do we say Python is dynamically typed?
Does a variable have a type?
What actually has the type?
What changes during an assignment?
Exercise 2 — Memory Tracing

Without running the code:

x = 10

y = x

x = "hello"

Conceptually answer:

After the first line, what does x reference?
After the second line, how many names reference the integer?
After the third line, what does x reference?
What does y reference?
Did the integer object change?
Exercise 3 — Following the Timeline

Consider:

value = [1, 2]

other = value

value = [3, 4]

Without running it:

Which object is created first?
Which names point to it?
What happens during the last assignment?
Which object does other reference at the end?
Why?
Exercise 4 — AI Engineering Thinking

Imagine:

model = load_model()

cached_model = model

model = fine_tune(model)

Conceptually explain:

Does fine_tune() change what cached_model references?
What actually changes when model = fine_tune(model) executes?
Why is this distinction important when building AI systems with multiple models (e.g., base model, fine-tuned model, evaluation model)?

This lesson is the foundation for the next one, Lesson 3 — Type Objects.

There, we'll answer an even deeper question:

If int, list, and str define behavior... what are they, really?

The answer is surprisingly Pythonic: they are objects too.