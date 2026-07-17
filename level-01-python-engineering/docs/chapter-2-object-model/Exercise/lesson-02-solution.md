# Exercises
## Exercise 1

In your own words:

What is the difference between:

equality
identity

Do not mention the operators yet.
Explain the concepts.

Equality means two things have the same value or content. It answers the question: "Do these two things look the same and hold the exact same data?

Identity means two things are the exact same physical object in memory. It answers the question: "Are these two names pointing to the same single entity, or are they separate entities?"

## Exercise 2

Suppose:

x = 10
y = x

Conceptually:

Are x and y equal?
Do they have the same identity?

Explain why.

Are they equal? Yes. Both x and y point to data representing the value 10.

Do they have the same identity? Yes. Because of the assignment y = x, the name y is bound to the exact same memory object that x is already pointing to. They share one physical identity.

## Exercise 3

Imagine:

Object A (10)

Object B (10)

They are two different objects.

Answer conceptually:

Equal?
Same identity?

Explain.


Equal? Yes. Both objects contain the same data value (10).

Same identity? No. They are two distinct objects occupying different spaces in memory. They are twins, not the same person.

## Exercise 4

Why would using identity instead of equality cause bugs when checking things like passwords or usernames?

Think about what you're actually trying to compare in those situations.


When validating a username or password, you care about equality (the text characters matching).

If you check for identity, the check will fail. A username typed into a login box by a user creates a brand new string object in memory. Even if the typed characters match the database string perfectly, they are two separate objects in memory. Checking identity would reject the correct password because the two strings live at different memory addresses.

## Exercise 5 (Thinking)

Suppose Python had only ==.

There was no concept of identity.

Name at least three programming problems that would become much harder.

Think about:

shared objects
memory
debugging
caching


Inability to track shared mutable state: You could not easily check if two separate parts of a program are modifying the exact same list or database connection, leading to untraceable bugs where data changes unexpectedly.

Broken caching systems: Cache tools could not instantly check if they have already processed a specific object instance without deeply inspecting all of its internal data.

Infinite loops during debugging: If you try to print or inspect a complex data structure that contains a reference to itself (a cyclical reference), a system based only on equality would get stuck in an endless loop trying to compare the data inside itself forever.


## Exercise 6 (Challenge)

Imagine Python had only is.

There was no equality.

What kinds of everyday programming tasks would become frustrating or impossible?

Think about:

numbers
strings
user input
database records



User input validation becomes impossible: You could never verify if a user typed "admin" because their typed string object would never share a memory identity with your hardcoded "admin" string object.

Math and calculations break down: A calculated result like 2 + 2 creates a number object. You could not easily compare it to a 4 fetched from a file or database because they would be different object instances.

Database and file processing fails: When loading records from a database, every row becomes a new object. You would be unable to check if a record loaded today matches a record loaded yesterday, even if every column contains identical data.