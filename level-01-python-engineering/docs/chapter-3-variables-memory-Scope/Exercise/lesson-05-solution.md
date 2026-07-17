# Exercises

As usual, don't run the code. Build the answer from the mental model.

## Exercise 1 — Why Nested Functions?

In your own words:

Why would a programmer define a function inside another function instead of making it global?

Don't just say "organization."

Think about:

encapsulation
readability
accidental misuse
software architecture


Encapsulation & State Capture: Nested functions can access variables from the outer function's scope without using global state. This creates a closure, allowing a helper function to carry hidden context (like a target hardware device or hyperparameter config) along with it wherever it is passed.

Accidental Misuse Prevention: By burying a helper function inside an outer function, you physically hide it from the rest of the codebase. Other developers cannot accidentally call it out of context, protecting the internal mechanics from being misused or relied upon elsewhere.

Architecture & API Minimisation: It keeps the public-facing API of a module clean. If a specific processing step is only ever relevant to one mathematical transformation, keeping it nested ensures that your module only exposes the primary tool, lowering the architectural complexity.

Readability & Locality: It establishes clear intent. When a function lives inside another, a reader immediately knows its lifecycle and scope are strictly tied to the parent function, eliminating the need to hunt through the rest of the file to see where else it might be used.


## Exercise 2 — Conceptual Namespaces

Consider:

def outer():

    def inner():
        pass

    inner()

Conceptually answer:

How many function objects exist after outer is defined?
Is inner available everywhere?
When does the name inner exist?
Which namespace owns the name inner?


How many function objects exist after outer is defined? 
Exactly 1 (the outer function object itself). The inner function object does not exist yet; it is only a blueprint inside outer's code body.

Is inner available everywhere? No. It is entirely hidden from the outside world and cannot be accessed from the global scope or other modules.

When does the name inner exist? The name inner only exists dynamically while outer() is actively executing. It is created fresh on the heap every single time outer() is called, and it vanishes (is garbage collected) as soon as outer() finishes running.

Which namespace owns the name inner? The Local namespace (the execution stack frame) of the active outer() function call.


## Exercise 3 — Architecture Thinking

Imagine Python did not support nested functions.

Every helper function had to be global.

Describe at least four problems this would create in a large AI project involving:

preprocessing
training
evaluation
logging
checkpointing

Think about namespace pollution, maintenance, readability, accidental use, and API design.


Severe Namespace Pollution and Naming Collisions:Preprocessing, training, evaluation, and checkpointing all require similar trivial utilities (e.g., normalize(), format_log(), validate_dimensions()). If everything must be global, you cannot use these simple names. You would be forced to invent exhausting, verbose names like _preprocess_image_tensor_normalize() and _checkpoint_save_weights_validate_dimensions() just to prevent names from overriding each other in the module dictionary.

Degraded API Discoverability and IDE Chaos:When a developer imports your pipeline module or types a dot (.) for autocomplete, the IDE will suggest dozens of internal, brittle mathematical helpers alongside the actual public functions like train() or evaluate(). This obscures the actual entry points of your application and ruins the user experience of your codebase.

High Vulnerability to Accidental Out-of-Context Execution:A specialized tensor-cropping helper built specifically for the quirks of the preprocessing data pipeline might accidentally be imported and called inside the evaluation or checkpointing steps. Because it is globally visible, Python will execute it perfectly fine—but it will silently corrupt evaluation metrics or save un-cropped checkpoints, introducing silent algorithmic bugs that are incredibly difficult to track down.

Brittle Maintenance and Monolithic Files:In large AI projects, models change frequently. If a helper function is global, a developer modifying the training step cannot easily tell if that helper is safely deletable or if it is secretly being used by logging or evaluation. Every single helper function becomes a global dependency, freezing your code structure and making it terrifying to refactor because you can no longer modify code with local confidence.