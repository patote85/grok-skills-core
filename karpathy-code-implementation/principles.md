# Detailed Principles

## 1. Read Before You Write
The biggest source of bad LLM code is not reading the existing codebase.
- Read the files you will modify.
- Observe how similar things are already done.
- Check imports and tests.
- If no clear pattern exists, say so and ask.

## 2. Think Before You Code
- State hypotheses and tradeoffs explicitly.
- Present 2-3 viable approaches when they exist.
- Stop and ask when confused. Do not invent plausible code.

## 3. Simplicity First
Write the minimum code that solves the specific problem.
Avoid premature abstraction, speculative error handling, unnecessary configurability and dead flexibility.

Test: if the only justification is “in case we need it later”, you over-engineered.

## 4. Surgical Changes
- Diff must be the smallest possible.
- Do not touch what was not requested.
- Match existing style.
- Clean only what *your* changes made orphan.
- Do not reformat the whole file.

## 5. Goal-Driven Execution + Verification + Reflection
Transform vague tasks into verifiable criteria before starting.
For non-trivial changes, perform a quick self-critique before presenting:
- Is this the simplest possible solution?
- Did I touch anything unrelated?
- Is every line of the diff justified?
- Do tests cover the main case and important edges?
- Did I follow existing project patterns?

Prefer running tests, inspecting the diff and checking types over trusting the model’s opinion.
