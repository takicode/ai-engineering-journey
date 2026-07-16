 # Exercises
## Exercise 1

What is the difference between:

a program,
and a process?

A Program: Passive data stored on your hard drive (SSD/HDD). It is just a file containing dormant instructions (like python.exe or app.py). It does nothing on its own.

A Process: An active, living instance of a program in execution. When you run a program, the operating system creates a process, which is a dedicated sandbox in memory where those instructions actually run

## Exercise 2

Why does the operating system create a process before your code runs?

Computer needs to manage multiple applications at once without them crashing into each other. The operating system creates a process to allocate a secure boundary (isolated memory space, environment variables, and file handles) for Python. Without this setup phase, the CPU would not know where to safely load the program instructions or store your application's data 

## Exercise 3

Why is parsing necessary before execution?

Computers cannot guess intent; they require absolute structure. Parsing takes a raw stream of characters and verifies that they follow the strict grammar rules of the language. It organizes them so the computer can systematically translate the human logic into operational instructions. Without parsing, a typo like prnt("Hello") would crash the machine at a deeper hardware level instead of throwing a clean software error


## Exercise 4

Arrange these in order:

Parse
Create Process
Compile to Bytecode
Execute Bytecode
Output
Cleanup

Explain each step.

Create Process: The OS allocates memory, sets up a secure sandbox, and loads the Python interpreter executable into RAM.

Parse: The Python interpreter reads the text of your .py file, breaks it into tokens, and checks it for correct grammar rules.

Compile to Bytecode: The interpreter converts the parsed grammar tree into low-level, compact numeric instructions (bytecode) that the virtual machine can read.

Execute Bytecode: The Python Virtual Machine (PVM) steps through the bytecode, translating it into instructions that your physical CPU runs.

Output: The CPU sends a system call to the OS, which triggers the hardware components (like your monitor) to display the results.

Cleanup: The program finishes. The OS tears down the process, reclaims the allocated RAM, and closes any open file 


## Exercise 5

When Python executes:

x = 10

Does Python simply store the number 10 inside x?
No, Python does not simply drop the number 10 into a memory slot labeled x.Python is an object-oriented language. When you run x = 10, Python creates a heavy structure in RAM called an Integer Object.

## Exercise 6 (Thinking)

Suppose your program crashes halfway through execution.

Does the original app.py file change?

Why or why not?

No, the original app.py file remains completely unchanged.

Why? When you run a script, Python only reads the text from app.py at the very beginning to load it into RAM. The execution happens entirely within the volatile memory (RAM) allocated to the process. Unless your code explicitly includes commands to open and overwrite its own source file on the SSD (which is highly unusual), a crash only destroys the live process in RAM


## Exercise 7 (Challenge)

Imagine two terminals both run:

python app.py

at the same time.

Do they share the same process?

Do they share the same RAM?

Do they share the same process? No. The operating system creates two completely separate processes, each with its own unique Process ID (PID).

Do they share the same RAM? No. Modern operating systems use Virtual Memory to enforce strict memory isolation. Process A cannot see, read, or overwrite the memory allocated to Process B. Even though both processes are reading the exact same source code from the SSD, they operate in completely distinct sandboxes in RAM. If Process A changes a variable, Process B remains completely unaffected






