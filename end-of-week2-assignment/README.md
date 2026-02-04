# End of Week 2 Assignment

Assignment Title:
Understanding Software Construction and Collaboration

Tasks:
1. Explain the difference between programming and software construction using one real-world example.
2. Describe a situation where poor maintainability could cause serious problems.
3. Explain why version control is critical in team-based software development.
4. Describe how code reviews improve both software quality and developer skills.
5. Reflect briefly on how Al can help in understanding code without replacing learning.


### Gareth Neville Kisuze S23B23/029 – Contribution
Part 1: Programming vs Software Construction (Real-World Perspective)*  
Programming focuses on writing code that performs specific tasks—implementing algorithms, processing inputs, and producing outputs. It’s mainly concerned with making individual components work correctly.

Software construction goes beyond writing functional code and involves building complete systems that can operate reliably in real environments. This includes system architecture, modular design, error handling, security considerations, performance optimization, testing, documentation, deployment, and long-term maintenance.

A real-world example is implementing a login feature. In a small student project, you might simply compare a username and password in a database and return “success” or “fail.” That is programming.

In production software, the same login feature becomes software construction work because it requires:
- Secure password hashing (not storing plain passwords)
- Protection against SQL injection and brute-force attempts
- Session/token management (e.g., refresh tokens, expiry)
- Logging and monitoring suspicious activity
- Handling network/database failures gracefully
- Automated tests for edge cases (timeouts, invalid states, rate limits)

Programming makes it run; software construction makes it survive real users, real risks, and constant change.

## Derrick Katende S23B23/024 – Contribution

[Paste your markdown answers here]

---

## Andrew Ogwang S23B23/050 – Contribution
### Part 3: Why Version Control Is Critical in Team-Based Development
Version control systems (such as Git and GitHub) help teams manage changes in software projects.  

In team development, many people work on the same codebase. Version control:
- Tracks every change made to the project
- Prevents team members from overwriting each other’s work
- Allows multiple features to be developed at the same time using branches
- Makes it possible to restore older versions if something breaks  

Without version control, collaboration becomes difficult. Files may be lost, changes may conflict, and the team can't properly build software together.  
Version control creates structure, accountability, and safety in teamwork.

---

### Nziriga Isaac Nickson S23B23/046 – Contribution
Part 4: How Code Reviews Improve Software Quality and Developer Skills*  
Code reviews are a quality gate and a learning mechanism. They introduce a second set of eyes before code becomes part of the main system.

How code reviews improve software quality:
- Catch logic errors early (before production)
- Identify security issues (unsafe inputs, auth flaws)
- Improve performance (inefficient loops/queries)
- Enforce standards and consistency (readability matters at scale)
- Reduce technical debt by challenging messy shortcuts

How code reviews improve developer skills:
- Developers get feedback on design and implementation choices
- People learn patterns used across the team (shared mental model)
- Junior developers improve faster by seeing real examples
- Teams share knowledge—no single developer becomes a bottleneck

In mature engineering teams, code reviews are one of the cheapest and most effective ways to improve reliability while building stronger engineers.

## Mutumba Benjamin S23B23/010 – Contribution

*Part 5: How AI Can Help Understand Code Without Replacing Learning*  
AI can support learning best when it acts like a tutor—not a replacement for thinking. It’s useful for understanding unfamiliar code, but it becomes harmful when it replaces the student’s reasoning.

Good use of AI in code learning includes:
- Explaining syntax and concepts in simpler terms
- Walking through a function line-by-line
- Suggesting alternative implementations and why they’re better
- Helping debug by pointing out likely failure points
- Generating small examples to test understanding

Responsible use means the learner still:
- Predicts what the code should do before running it
- Writes their own solution attempts first
- Uses AI to clarify gaps, not to skip the work
- Validates AI suggestions by testing and reading documentation

Used properly, AI increases understanding and reduces time spent stuck. Used poorly, it produces “working code” without real comprehension—making the learner weaker in interviews, debugging, and real projects.


