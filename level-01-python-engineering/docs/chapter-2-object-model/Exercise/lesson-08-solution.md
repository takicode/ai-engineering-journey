# Exercises
## Exercise 1

In your own words:

What is string interning?

Why does Python use it?

What is it? It is an optimization technique where Python stores only one copy of distinct, immutable string values in an internal lookup table (dictionary).

Why does Python use it? It saves memory by avoiding duplicate string objects. It also speeds up string comparisons; checking if two variables point to the exact same memory location (is) is much faster than comparing long strings character-by-character (==).

## Exercise 2

Suppose:

a = "python"
b = "python"
c = "python"

Draw the memory conceptually using ASCII.

Answer:

How many string objects exist (conceptually, if the string is interned)?
How many names exist?
What is the reference count of the "python" object (ignoring Python's internal references)?


            "Python"
          /    |    \
         /     |     \
        a      b     c
                  
How many string objects exist? Exactly 1 object.
How many names exist? There are 3 names (a, b, and c).
What is the reference count? 3


## Exercise 3

Why doesn't Python intern every string ever created?

Imagine a web server generating millions of unique session IDs every day.

Explain what would happen if Python permanently interned all of them.


Why it's limited: Interning requires keeping strings in a global lookup table forever (or until the program ends). Interning every string would quickly exhaust system memory.

The Web Server Scenario: If a web server permanently interned millions of unique session IDs daily, those strings would never be garbage collected. Memory usage would grow continuously until the server ran out of RAM and crashed.

## Exercise 4

Suppose two variables contain the text:

"OpenAI"

Why should you still use == instead of is when comparing them?

What is the difference between the two questions being asked?

Why use == instead of is? Python only automatically interns strings that look like valid Python identifiers (letters, numbers, underscores). 

While "OpenAI" might be interned in some versions or context blocks, it is not strictly guaranteed by the language. Using is will randomly fail depending on how the code is compiled or executed.

The difference between the two questions:
a == b asks: "Do these two variables contain the same text characters?" (Value comparison)

a is b asks: "Do these two variables point to the exact same spot in memory?" (Identity comparison)

## Exercise 5 (Thinking)

Imagine strings were mutable.

How would that affect:

string interning,
memory usage,
shared references,
program correctness?

Would Python still be able to safely share one "admin" object among thousands of variables?

Explain your reasoning.


String Interning: It would become impossible. Python could no longer safely use a central lookup table for strings.

Memory Usage: RAM usage would spike because Python would have to create a brand-new, isolated string object for every single variable to prevent cross-contamination.

Shared References & Correctness: If thousands of variables shared one "admin" object, changing the value of one user's role to "user" would instantly change everyone else's role to "user" too, completely breaking security and program correctness.

## Exercise 6 (Challenge)

A developer says:

"Since Python interns strings, I can use is for every string comparison."

Write a response correcting this misunderstanding.

Explain:

why string interning exists,
why it is an implementation optimization,
why relying on it makes code fragile,
why == expresses the programmer's real intent.

The Correction: Do not use is for standard string comparisons. It introduces silent, hard-to-find bugs because Python does not intern every string.

Why interning exists: It exists as an internal optimization for Python's own speed (like looking up variable names and function attributes quickly), not as a tool for developers to change how they compare text.

Why it makes code fragile: Python's automatic interning rules are an implementation detail. They can change between different versions of Python (e.g., CPython vs. PyPy) or even change depending on whether you run code in a single file versus an interactive terminal shell.

The Programmer's Intent: When comparing text, your actual goal is to check if the string contains the correct words or characters (==). Using is tells the computer to check memory hardware layout, which has nothing to do with the meaning of your data.