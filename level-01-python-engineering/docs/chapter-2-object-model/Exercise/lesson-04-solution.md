## Exercise 1

In your own words:

What is the difference between:

rebinding a name
mutating an object

Use your own examples.


Rebinding a name means moving a variable label from one object to a completely different object in memory. The original object stays exactly as it was.

Example: You have a variable car = "Toyota". Later, you write car = "Ford". You did not turn the Toyota into a Ford; you simply moved the car label to a fresh, new string object.

Mutating an object means changing the internal data inside the existing object without moving the name label. The object keeps its exact same memory identity.

Example: You have a shopping list variable cart = ["apples", "milk"]. You add an item: cart.append("bread"). The name cart still points to the exact same list object in memory, but that list object now contains three items instead of two.

## Exercise 2

Consider:

x = 10

y = x

x = x + 5

Draw the memory conceptually.

Answer:

How many integer objects exist at the end?
Which object does each name point to?
Did any object change?

    Names (Variables)         Memory Objects
    +---------------+         +--------------+

    |       x       | ------> |  Integer 15  |  (New object from math operation)
    +---------------+         +--------------+

    +---------------+         +--------------+

    |       y       | ------> |  Integer 10  |  (Original object)
    +---------------+         +--------------+

How many integer objects exist at the end? Two objects (10 and 15).

Which object does each name point to? x points to 15. y points to 10.

Did any object change? No. Integers are immutable. Python evaluated x + 5 (which is 10 + 5), created a completely new integer object 15, and rebound the name x to it.

## Exercise 3

Now consider:

numbers = [1, 2]

backup = numbers

numbers.append(3)

Draw the memory.

Answer:

How many list objects exist?
Which names point to each object?
Did the object's identity change?
Why does backup also "see" the new value?

## Exercise 4

Why are immutable objects generally safer for things like:

passwords,
usernames,
dates,
configuration values?

Think about shared references and accidental modification.

Immutable objects are safer because they guarantee data integrity across shared references.If usernames, passwords, dates, or configuration values were mutable, a malicious or poorly written function could modify an object passed to it. 

For example, if a configuration object CONFIG = {"timeout": 30} was passed to a network function, and that function accidentally mutated "timeout" to 0, it would break the configuration for the entire application.

With immutable objects, you can share a reference with 100 different parts of a program without worrying that one part will accidentally alter the data for everyone else.

## Exercise 5 (Thinking)

Suppose Python made lists immutable.

How would that affect:

appending items,
sorting,
removing elements,
AI training,
large datasets?

Would programs become simpler?

Or slower?

Or both?

Explain your reasoning.

If lists were immutable, everyday operations would change dramatically:Appending, sorting, and removing elements would no longer modify the list in place. Instead, every single .append(), .sort(), or .remove() operation would be forced to copy the entire existing list into a brand-new list object with the modification applied.

AI training and large datasets would become incredibly slow and memory-intensive. Modifying a dataset of 1 million items to update a single value would require duplicating all 1 million items in memory.

Would programs become simpler, slower, or both?Both.They would become simpler because you would eliminate all bugs related to shared mutable states (aliasing bugs). 

You could safely pass lists around without fearing accidental modifications.They would become dramatically slower and consume massive amounts of extra RAM, because the CPU would waste immense processing cycles constantly copying data structures for basic updates.

## Exercise 6 (Challenge)

A student says:

"Variables are mutable because I changed x from 10 to 20."

Correct this statement carefully.

Explain:

what actually changed,
what stayed the same,
why Python behaves this way.


"I understand why it feels like the variable is mutable, but there is a crucial distinction to make here: Names change, but integer objects do not.

When you move from x = 10 to x = 20, here is exactly what changes and what stays the same:

What changed: Only the assignment of the name label x. It stopped pointing to the object 10 and started pointing to a completely different object 20.

What stayed the same: The integer object 10 itself did not change or transform into 20. It remains in memory exactly as it was.

Python behaves this way because numbers are immutable. By making numbers unchangeable, Python ensures that if five different variables are currently pointing to the number 10, reassigning x to 20 will safely leave the other four variables pointing to 10 completely undisturbed."