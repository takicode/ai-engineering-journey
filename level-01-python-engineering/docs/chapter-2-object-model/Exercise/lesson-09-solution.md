# Exercises

As usual, don't run the code. Reason it out.

# Exercise 1

In your own words:

What is the difference between a shallow copy and a deep copy?

Do not mention Python functions yet.

Use your own analogy.


Shallow Copy: You buy a brand-new photo album and fill it with exact duplicates of the slips of paper pointing to where the original photos are kept. If you add or remove a photo from your new album, the original album is unaffected. However, if you take a marker and draw a mustache directly onto a photo in your new album, the photo in the old album now has a mustache too—because both albums still point to the exact same physical photographs.

Deep Copy: You buy a new photo album, take every single photograph out of the original album, run them all through a high-quality photocopier, and place the brand-new duplicate prints into your new album. The two albums are completely isolated. Scribbling on a photo in the new album has zero effect on the original album.

# Exercise 2

Suppose conceptually you have:

Original List

↓

Apple
Banana
Orange

You make a shallow copy.

Draw the memory using ASCII.

Answer:

How many list objects exist?
How many fruit objects exist?
Which objects are shared?


           A ───┐
                │
                ▼
                Apple
                Banana
                Orange
                ▲
                │
          B ────┘

How many list objects exist? Exactly 2 list containers.

How many fruit objects exist? Exactly 3 fruit string objects.

Which objects are shared? All 3 fruit objects are shared between both lists.

# Exercise 3

Now imagine you make a deep copy instead.

Draw the memory.

Answer:

How many list objects exist?
How many fruit objects exist?
Are any objects shared?

    A

    ↓

    Apple
    Banana
    Orange

    ----------------

    B

    ↓

    Apple
    Banana
    Orange


How many list objects exist? 2 list containers.

How many fruit objects exist? 6 fruit string objects.

Are any objects shared? No objects are shared.

# Exercise 4

Why is a shallow copy usually much faster than a deep copy?

Think about:

CPU work
memory allocation
AI datasets
images
machine learning models

Shallow copying only duplicates a flat array of memory pointers, completely ignoring how large or complex the underlying data is.

CPU Work & Memory: A shallow copy only takes a fraction of a microsecond because the CPU allocates a tiny block of memory for the pointers. A deep copy forces the CPU to recursively crawl through every single layer of data, spawning millions of new allocations.

AI & Machine Learning: AI datasets and images consume gigabytes of RAM. A machine learning model contains billions of weights. Shallow copying allows you to re-organize, slice, or filter a dataset instantly without duplicating those massive gigabytes of underlying matrix data.


# Exercise 5 (Thinking)

Imagine Python automatically performed a deep copy every time you passed a list into a function.

What problems would this create for:

AI training
web servers
databases
large files

Try to think beyond "it would be slower."

AI Training: Training would become impossible. If you passed a 50GB dataset into a training loop function, Python would attempt to copy all 50GB into a new RAM block on every single iteration, immediately triggering out-of-memory crashes.

Web Servers: Web servers handling incoming JSON lists would choke under heavy loads. Instead of passing data streams efficiently between processing functions, the server would exhaust its CPU cycles endlessly duplicating user requests.

Databases: In-memory databases or cache layers would become useless. Databases rely on functions to modify a shared state or index. Deep-copying everything means changes made inside a function would be lost, never reflecting in the main database.

Large Files: Processing giant log files or video frames line-by-line would ground to a halt, as every data-manipulation helper function would freeze the system to clone the entire file structure


# Exercise 6 (Challenge)

A student says:

"A shallow copy is useless because it doesn't really copy anything."

Write a response correcting this misunderstanding.

Explain:

what is actually copied,
why that is often exactly what programmers want,
why deep copying everything would often be a terrible idea.


The Correction: Shallow copies are incredibly useful and represent one of the most vital performance features in Python. They absolutely do copy something: they copy the structural layout (the container itself).

What is actually copied: The outer container is brand new. This means you can sort the new list, reverse it, append new items, or delete items without changing the order or contents of the original list.

Why it's what programmers want: Most of the time, developers want to manipulate the collection structure (e.g., filtering out unwanted rows or sorting a table) while keeping the actual heavy data objects safely untouched in memory.

Why deep copying everything is a terrible idea: Deep copying everything by default destroys performance. It introduces massive, unnecessary memory overhead and separates objects that should remain connected. If you want multiple lists to reflect live updates to a shared configuration object, a deep copy would break that connection entirely.