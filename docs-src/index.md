# Novus, from zero to real projects

<div class="hero-panel">
  <p class="eyebrow">Systems language · native binaries · package-managed workflow</p>
  <h1>Start with a clean hello world. End with a real game and a real app.</h1>
  <p class="hero-lead">
    This guide is not a vague overview. It walks through <strong>installing Novus and Nox</strong>,
    creating a project, using <code>std</code>, writing inline assembly, and understanding how
    real Novus codebases are structured.
  </p>
  <div class="hero-actions">
    <a class="hero-button" href="guide/install/">Install Novus</a>
    <a class="hero-button ghost" href="guide/first-project/">Make your first project</a>
  </div>
</div>

## What this repo covers

<div class="quick-grid">
  <a class="quick-card" href="guide/first-project/">
    <strong>First project</strong>
    <span>From <code>nox init</code> to your first compiled binary.</span>
  </a>
  <a class="quick-card" href="guide/language-tour/">
    <strong>Language tour</strong>
    <span>Modules, imports, functions, arrays, strings, overloads, and <code>#if</code>.</span>
  </a>
  <a class="quick-card" href="guide/inline-assembly/">
    <strong>Inline assembly</strong>
    <span>How Novus uses <code>mov</code>, <code>getreg</code>, <code>syscall</code>, and <code>win_call</code>.</span>
  </a>
  <a class="quick-card" href="guide/working-with-std/">
    <strong>Working with std</strong>
    <span>The standard library entrypoint, common helpers, and practical code patterns.</span>
  </a>
  <a class="quick-card" href="walkthroughs/platformer/">
    <strong>Platformer walkthrough</strong>
    <span>Follow the rendering loop, input handling, camera, and window API.</span>
  </a>
  <a class="quick-card" href="walkthroughs/todo-app/">
    <strong>Todo app walkthrough</strong>
    <span>See a simple CLI app parse arguments and persist data to disk.</span>
  </a>
</div>

!!! note "Compatibility snapshot"
    These docs were written against the currently installed toolchain on this machine:

    - **Novus compiler:** `V0.2.0`
    - **Novus repo:** `753ee3c`
    - **Nox repo:** `632c8be`
    - **window library:** `1.1.1`
    - **std examples:** based on current ecosystem usage in the linked repos

## Recommended reading order

1. [Install Novus and Nox](guide/install/)
2. [Your First Project](guide/first-project/)
3. [Language Tour](guide/language-tour/)
4. [Working with std](guide/working-with-std/)
5. [Nox and Libraries](guide/nox-and-libraries/)
6. [Inline Assembly](guide/inline-assembly/)
7. Project walkthroughs

## When to use the AI docs

If you are building tooling, generating Novus code automatically, or teaching an AI agent how to reason about a Novus repo, start with:

- [AI reference](ai/ai-reference/)
- root-level [AI_GUIDE.md](https://github.com/MJDaws0n/Novus-Getting-Started/blob/main/AI_GUIDE.md)
- root-level [llms.txt](https://github.com/MJDaws0n/Novus-Getting-Started/blob/main/llms.txt)

## Related repositories

- [Novus](https://github.com/MJDaws0n/Novus)
- [Nox](https://github.com/MJDaws0n/Nox)
- [Todo-App](https://github.com/MJDaws0n/Todo-App)
- [platformer-game](https://github.com/MJDaws0n/platformer-game)
