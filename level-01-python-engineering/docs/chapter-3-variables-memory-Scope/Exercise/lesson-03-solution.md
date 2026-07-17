Exercises

As before, don't run the code. Build the answer from your mental model.

Exercise 1 — Understanding Global Scope

In your own words:

What does "global" actually mean in Python?
Does "global" mean the object itself lives in a special place?
Where does the object live?
Where does the name live?

What "global" means: In Python, "global" is strictly scoped to the module level. It does not mean "global to the entire program" (unless everything is in one file). It simply means the name is accessible anywhere within that specific .py file.

Special place for the object: No. The object itself does not care if it is referenced by a local variable or a global variable. It does not get moved to a special "global zone" in memory.

Where the object lives: All objects live on the private heap.Where the name lives: The global name lives as a string key inside the module's namespace dictionary (the __dict__ attribute of the module object), which also resides on the heap.



## Exercise 2 — Reasoning About Namespaces

Consider:

x = 100

def show():
    print(x)

Conceptually answer:

How many namespaces exist before show() is called?
How many exist while show() is executing?
Where is the name x found?
Is the integer 100 copied into the function?

Before show() is called: Only the global namespace exists. This is where your top-level variables and function definitions live. It contains the names x and show.

While show() is executing: A local namespace is created specifically for that function run. This namespace is empty, as there are no variables or arguments defined inside show. However, the global namespace is still active, making a total of two.

Where x is found: Python searches for names Since x is not defined inside the function (Local), Python checks outside the function in the main module (Global), where it finds x = 100.

No copying of the integer 100: Python handles names like tags or labels attached to objects, not as physical boxes holding data. When print(x) executes, the function simply follows the name x to look up the shared integer 100 in memory


## Exercise 3 — Architecture Thinking

Suppose an AI application stores these as globals:

model
config
learning_rate
dataset

Now imagine 20 different functions can freely modify them.

Describe at least four long-term software engineering problems this design would create.

Focus on maintainability, debugging, testing, scalability, and correctness—not just "variables can change."


Loss of Determinism and Order-of-Execution Bugs (Correctness):Because any function can modify the learning_rate or config, the application's behavior becomes completely dependent on the exact order in which functions are called. If Function A modifies the config, Function B will behave differently depending on whether it runs before or after Function A. This creates intermittent, "haunted" bugs that are nearly impossible to reproduce consistently.

Extreme Testing Rigidity and "State Poisoning" (Testing):To unit test just one function, you can no longer test it in isolation. You have to manually set up the exact global state of all four variables before the test. Furthermore, if Test 1 modifies the global model, it will "poison" the state for Test 2, leading to cascading test failures across your test suite unless you write heavy setup/teardown boilerplate to reset the globals every time.

Concurrency and Parallelism Hard Blockers (Scalability):If you ever need to scale the application to handle multiple requests or data streams concurrently (using threads or asynchronous programming), these globals create immediate race conditions. Two threads trying to update or read the model or dataset at the same time will corrupt the data or cause crashes, forcing you to use complex locks that destroy performance.

Cognitive Overload and Exploding Dependency Web (Maintainability/Debugging):When a developer wants to update how config works, they cannot just look at one class or module. They must scan all 20 functions across the codebase to ensure they don't accidentally break hidden assumptions. The "surface area" of what a developer must hold in their head expands exponentially, making refactoring or onboarding new developers incredibly risky.