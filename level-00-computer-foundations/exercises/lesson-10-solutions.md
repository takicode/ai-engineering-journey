# Exercises
## Exercise 1

In your own words:

Why was assembly language invented?
Assembly language was invented to replace those binary numbers with short, memorable english abbreviations (like ADD or MOV), making programming significantly faster and less prone to human error.

Exercise 2

What is the difference between:

Machine Language consists entirely of raw binary numbers (10110000 00001010). It is understood directly by the CPU hardware but is unreadable to humans.

Assembly Language uses human-readable text shortcuts called mnemonics (MOV AL, 10). It represents the exact same step-by-step instructions as machine language, but in a format humans can easily read

Exercise 3

What does an assembler do?
An assembler is a translation program. Its sole job is to take a text file written in assembly language and translate it, line-by-line, into the raw binary machine language that the CPU can execute.

Exercise 4

Why can't a CPU execute assembly language directly?
A CPU is a physical chip made of electronic circuits and transistors. It can only respond to electrical voltage signals (on/off states represented as binary). Because assembly language is made of text characters (like the letters A, D, D), the physical hardware has no way to process it until it is converted into binary digits

Exercise 5

Suppose you see:

Describe, in plain English, what is happening.

MOV R1, 10: Move (copy) the number 10 into register R1.
MOV R2, 20: Move (copy) the number 20 into a second register R2.
ADD R1, R2: Add the value in R2 to the value in R1, and store the final result (30) back inside register R1

Exercise 6 (Thinking)

Why do you think modern operating systems are mostly written in C or C++, but still contain some assembly?
Modern operating systems need to strike a balance between development speed and absolute hardware control.

Exercise 7 (Challenge)

Suppose someone says:

"Assembly is unnecessary because Python already exists."

Do you agree?

No, I do not agree.While Python is fantastic for building web apps, data models, and scripts quickly, it relies entirely on a foundational software layer to exist.Without low-level languages like assembly, the very tools needed to run Python wouldn't exist.


