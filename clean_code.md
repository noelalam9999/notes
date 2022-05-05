## Why clean code
- Most software bugs are introduced when changing existing code. This is often because the developer who’s making the changes cannot fully grasp their effects.
- Clean code minimizes the risk of introducing defects by making the code as easy to understand as possible.
- The initial cost of change is a bit higher when writing clean code than quick and dirty programming, but is paid back very soon.
- Unclean code and lack of documentation result in technical debt that increases exponentially as the project grows.
- Writing clean code from the start in a project is an investment in keeping the cost of change as constant as possible throughout the lifecycle of a software product.

## Principles
- KISS (i.e. “keep it simple, stupid”). Break your system down into components that are of a size you can grasp within your mind. Write modular code, use composition, abstract logic into small and simple units. Each component should have a single responsibility, and be easy to understand.
- Separation of concerns and decoupling. Each component should interact with the others through an interface (i.e. methods, inputs and output), and not care about the internals of other components. This means that a change in one component, unless it modifies its interface, should not affect other components (e.g. switching the underlying db in a model).
- DRY (i.e. “don’t repeat yourself”) and single source of truth. When you write code, ask yourself “if someone needs to modify this feature later or read a certain information, in how many places would it need to be checked?” If the answer is more than one, refactor your code (e.g. wrap logic into reusable functions, keep constants in shared configuration files, use CSS variables, componentize UI elements, etc).
- Use naming wisely. Files, variable and function names should be as descriptive, accurate, and easy to understand as possible (e.g. instead of directly passing 3600000 to setTimeout(), assign it first to a variable named oneHourInMs).
- Add comments where necessary. If some logic is particularly complicated or counterintuitive, and can’t be further simplified, add a comment to help whoever might need to work on it in the future (it could be you).
- Always write docs, and keep them in sync with your code any time it’s modified. Have a written high-level guide that can be referenced by you or other people in your team to use or develop your app. It’s a good idea to document certain features or processes even before writing the actual code.
- Catch errors as closely as possible to their source (aka “fail fast”), and react in a meaningful way (e.g. handle exceptions, notify the developer, collect stats, show a message to the user, etc).
- Implement automated tests, starting from the components that are most important or likely to break, and write code so that each component is testable in isolation (through decoupling and mocks).
- Structure tests in three sequential steps: arrange, act, assert. For each test, first prepare all the assets that are required to run it, then perform one action (the object of the test), then check your assertions to see if the test is passing.
- Add pre-commit hooks (e.g. code linting and test running) to your repos, and protect branches that should have working code by enforcing that any merge first passes the required checks.
- Delete unused things. Don’t keep code around if it isn’t used anywhere. It just adds up through time and makes your codebase more complex.
- Always have a running system. Change your system in small steps, from a running state to a running state. Commit one step at a time, with clear messages (even better if they follow a conventional format). This way it’s also easier to roll back if you have a problem.

## Code smells
- Are signals that something in your code is problematic. You should learn to detect these signals and refactor your code to fix the underlying issues. Here follows a short list.
- The software is difficult to change. A small change breaks the code in many places, and requires a cascade of subsequent changes to get it fixed.
- When there’s a bug, it often takes a long time to find its source and fix it.
- Files are too long, or contain code that addresses unrelated things.
- Tests and documentation are not present or don’t have adequate coverage.
- Code contains duplicates and repetitions, or it’s tightly coupled. Modifying a feature requires changes in many places, and the programmer is more likely to oversee something.
- Too many arguments to a function, usage of impure functions, or functions returning different data types.