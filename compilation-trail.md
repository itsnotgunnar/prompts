  For each compilation error:

  1. THE CLAIM
 The compiler is asserting something about reality.
 What is it asserting?
 (Not "there's an error" — what specific claim about the code?)

  2. THE CONTRADICTION
 This claim contradicts something you believed.
 What is the ONE belief being contradicted?
 State it precisely. If you can't state it, you don't know it.

  3. THE FALSIFICATION
 Assume your belief is wrong.
 What would the codebase look like if your belief were false?
 Go look for that world. Actively seek evidence against yourself.

 - If you believe "this function exists": search for evidence it doesn't,
   or exists only as a stub, or exists with the wrong shape
 - If you believe "this is the only version": search for duplicates
 - If you believe "this was finished": search for TODO, unimplemented!,
   empty bodies, panic placeholders

  4. THE VERDICT
 After honest falsification attempts:
 - FALSIFIED: Your belief was wrong. What is actually true?
 - SURVIVED: Your belief withstood scrutiny. The error is elsewhere.

  5. THE IMPLICATION
 If your belief was false, what else might be false?
 What other beliefs depended on this one?
 (This is where you discover the second error before the compiler does.)

  ---
  The Deeper Point

  The goal isn't to fix compilation errors faster.

  The goal is to update your mental model of the codebase so it matches reality.

  Every error fixed without updating the mental model is technical debt of understanding. You'll make the same category of mistake again because you still believe something false.

