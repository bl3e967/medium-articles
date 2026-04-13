# CLAUDE.md — Ghost-writing Guide for Benjamin Lee's Medium Articles

## Repository Overview

This repository contains the code and written content for articles published at
[medium.com/@bl3e967](https://medium.com/@bl3e967) and [towardsdatascience.com/@bl3e967](https://towardsdatascience.com/author/bl3e967/). Articles cover Data Science, Python, and software engineering — with
a recent focus on network graph visualisation, LLM agents, MCP servers, and coding best
practices for AI-assisted development.

Each article lives in its own folder, named after the article title. The main content is
written inside a **Jupyter notebook** (`.ipynb`) using markdown cells — this is the canonical
format. A short `README.md` may accompany the notebook as a companion file.

---

## Writing Style

This is the most important section. Match this style precisely.

### Voice & Tone
- **First-person, conversational, and direct.** Write as "I" and address the reader as "you".
- **Confident but grounded.** Make strong claims, but qualify them when appropriate
  ("A quick warning:", "I'd say this is most relevant for...").
- **Honest about trade-offs.** Don't oversell. If something is slow, say it's slow.
  If something has a flaw, name it.
- **Self-deprecating when appropriate.** Light humour works ("my cute little Macbook Air").
- **Purposeful.** Every sentence should earn its place. Avoid filler.

### Sentence & Paragraph Style
- Mix **short punchy sentences** with longer explanatory ones. Vary rhythm intentionally.
- Use **rhetorical questions** to drive the narrative, then answer them immediately.
  - e.g. "Why? Because the manual labor of writing code has been offloaded."
- Start paragraphs with **casual connectors** when it flows naturally: "So", "And", "But", "Now".
- Use **em dashes** and **colons** for dramatic effect or to introduce a point.
- Avoid padding words: no "very", "really", "quite", "essentially" without purpose.
- **British English spelling**: "recognise", "behaviour", "colour", "optimisations", etc.

### Structure Conventions
- Articles open with a **title + subtitle** (italicised tagline).
- Use a `## Why?` or `## Why read this article?` section near the top to justify the article's
  existence — this is a signature section.
- Use **numbered goals or sections** when outlining a project structure:
  ```
  ### 1. Run on my local computer
  ### 2. Replicate X functionality
  ### 3. Be quick
  ```
- Use `## <number>. <Section Title>` for major implementation sections.
- **Blockquotes** (`>`) for key insights or thesis statements.
- Use **"Good:" / "Bad:"** bullet summaries when comparing tools or approaches.
- End with a reference to future articles in the series when relevant.

### Code & Technical Content
- Embed code as **fenced Python/bash code blocks** in markdown cells.
- Accompany every significant code block with a brief plain-English explanation —
  before *and/or* after the code, never just dump code alone.
- When introducing a class or function for the first time, show a **skeleton/stub version**
  first, then fill in the details progressively.
- Use install commands in their own bash code block when setting up a library.
- Name specific tools, versions, and libraries. Be concrete.
- Explicitly discuss **why** a design decision was made, not just what it is.`

### Comparisons & Tool Evaluations
- When comparing multiple tools (e.g. TTS models, graph libraries), cover each with:
  - A short description + install or quickstart code snippet
  - "Good:" / "Bad:" bullet points
  - A brief verdict
- Be opinionated. Give a recommendation and explain it.

### Bullet Points
- Used liberally for lists of features, goals, pros/cons, and action items.
- Keep bullets concise — one clear idea per bullet.
- Avoid using bullets for narrative flow (use prose for that).

---

## Topic Areas

Articles cover:

- **Network graph visualisation** (NetworkX, gravis, pyvis, graph databases like Kuzu)
- **LLM Agents & AI tooling** (LangGraph, MCP servers, Ollama, local LLMs)
- **Software engineering for data scientists** (code smells, design patterns, abstraction)
- **Practical Python tooling** (comparisons of libraries, step-by-step tutorials)
- **Voice assistants / AI applications** (speech-to-text, TTS, local AI pipelines)

Articles are usually **tutorial-driven** or **problem to solution** in structure. They solve
a real, relatable problem the author personally encountered.

---

## Article Structure Template

```
# Title

## Short tagline / subtitle (not a header — use bold or italics in the first markdown cell)

## Why? (or "Why read this article?")
<Justify why this article exists. What problem does it solve? Who is it for?>

## Goals (optional, for project-based articles)
### 1. Goal One
### 2. Goal Two
### 3. Goal Three

## <Number>. Section Title
<Implementation or conceptual content>

### Sub-section
<Detail>

## Conclusion / Next Steps
<Brief wrap-up. Reference future articles in the series if applicable.>
```

---

## Notebook Conventions

- All article content is written in **markdown cells** within Jupyter notebooks.
- Code cells contain the actual runnable Python code demonstrated in the article.
- Keep notebook outputs for code cells that produce visualisations or useful terminal output —
  these appear inline when rendered on Medium.
- Image resources live in a `resources/` subdirectory within the article folder.
  Reference them as `![image](resources/filename.png)` in markdown cells.

---

## Things to Avoid

- **No fluff introductions.** Don't open with "In today's rapidly evolving world of AI..."
- **No over-hedging.** Say things clearly. Don't qualify every sentence into meaninglessness.
- **No passive voice unless natural.** Prefer "I built X" over "X was built".
- **No American spellings.** (e.g. "optimize" -> "optimise", "behavior" -> "behaviour")
- **No generic conclusions.** Don't end with "I hope you found this article useful!"
- **Don't explain the obvious.** Assume the reader is technical and intelligent.
- **Don't start with bullet points.** Ground the reader in narrative prose first.
