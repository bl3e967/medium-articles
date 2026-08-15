# CLAUDE.md — Working Guide for Benjamin Lee's Medium Articles

## Repository Overview

This repository contains the code and written content for articles published at
[medium.com/@bl3e967](https://medium.com/@bl3e967) and
[towardsdatascience.com/@bl3e967](https://towardsdatascience.com/author/bl3e967/). Articles cover
Data Science, Python, and software engineering — with a recent focus on network graph
visualisation, LLM agents, MCP servers, and coding best practices for AI-assisted development.

**This is a writing repository, not a software project.** There is no package, no test suite, no
CI, and no linting. The deliverable is prose. Code exists only to support the prose — it is
demonstration material for readers, not a library anyone imports.

Each article lives in its own folder, named after the article title. The main content is written
inside a **Jupyter notebook** (`.ipynb`) using markdown cells — this is the canonical format for
most articles. A short `README.md` may accompany the notebook as a companion file.

---

## Repository Structure

```
medium-articles/
├── README.md                            # Public index of published articles + Medium links
├── CLAUDE.md                            # This file
├── .gitignore                           # Python template + torch dataset/output ignores
│
├── An Interactive Visualisation for your Graph Neural Network Explanations/
│   ├── gnn_explanation_interactive_vis.ipynb
│   └── requirements.txt
├── Enhance Your Network Visualizations with the Power of a Graph DB/
│   ├── Enhance Your Network Visualizations with the Power of a Graph DB.ipynb
│   ├── memgraph-platform/docker-compose.yml   # Memgraph + Memgraph Lab, for running the demo
│   └── requirements.txt
├── The New Best Python Package for Visualising Network Graphs/
│   ├── gravis_demo.ipynb
│   ├── README.md
│   └── requirements.txt
├── The Two Best Tools for Plotting Interactive Network Graphs/
│   ├── comparison.ipynb
│   ├── Plots/*.html                     # Committed pyvis output — referenced by the article
│   ├── environment.yml                  # conda env "graph-comparison" (Python 3.10.12)
│   └── requirements.txt
│
├── spec driven development/             # In progress — spec-first layout (see below)
│   ├── draft.md
│   └── spec/GOAL.md
│
└── voice-assistant/                     # Series folder (see naming caveat below)
    ├── Creating my own voice assistant using langraph and mcp servers/
    │   ├── Creating my own Voice Assistant using LangGraph and MCP servers.ipynb
    │   └── resources/*.png|*.jpg
    ├── coding concepts to learn to handle coding agents properly/
    │   ├── draft.ipynb
    │   └── resources/*.jpg
    └── creating my own ai agent into a mobile app/
        └── draft.ipynb
```

### Two generations of article folder

The repo has drifted over time. Recognise which kind of article you're working in before editing:

**1. Runnable tutorial articles** (the four graph-visualisation folders at the root)

- Notebook mixes markdown prose with real, executed code cells.
- Cell outputs are **committed on purpose** — plots and terminal output render inline on Medium.
  Do not strip outputs.
- Pinned `requirements.txt` in the folder; sometimes an `environment.yml` or `docker-compose.yml`.
- Notebook filename varies: sometimes descriptive (`gravis_demo.ipynb`, `comparison.ipynb`),
  sometimes the full article title.

**2. Prose-first drafts** (everything under `voice-assistant/`, and `spec driven development/`)

- Notebooks are effectively **markdown-only** — 43 markdown cells and zero code cells in the
  published voice assistant article. No kernel metadata, never executed.
- Code appears as **fenced code blocks inside markdown cells**, not as executable code cells,
  because the underlying project lives in a separate repository.
- Work in progress is named `draft.ipynb` (or `draft.md`); a published article gets renamed to
  the article title.
- Images live in `resources/` and are referenced as `![image](resources/filename.png)`.

### Naming caveats — read before running shell commands

- **`voice-assistant/` is a series folder, not a topic folder.** It holds the voice assistant
  article plus two unrelated drafts (the coding-concepts curriculum piece and the mobile app
  piece). Treat it as "the current series of articles", not as voice-assistant-only content.
- **`Enhance Your Network Visualizations with the Power of a Graph DB`** contains a
  **non-breaking space (U+00A0)** before `DB`, in both the folder name and the notebook filename.
  A hand-typed path will fail with "No such file or directory". Glob it (`Enhance*/`) or use
  tab completion rather than retyping the name.
- Folder names contain spaces throughout. Always quote paths in shell commands.
- The one American spelling in the repo ("Visualizations") is in that published folder name and
  its Medium URL. **Leave it.** Renaming it breaks the link between repo and published article.
  British spelling applies to prose, not to historical folder names.

### File encoding gotcha

`The Two Best Tools for Plotting Interactive Network Graphs/requirements.txt` and
`environment.yml` are **UTF-16 encoded** (PowerShell `>` redirection on Windows). `cat` prints
them with spaces between every character and greps against them fail. Convert before reading:

```bash
iconv -f UTF-16 -t UTF-8 "The Two Best Tools for Plotting Interactive Network Graphs/requirements.txt"
```

Write any new dependency file as UTF-8.

---

## Development Workflows

### Adding a new article

1. Create a folder named after the working title (root level, or inside `voice-assistant/` if it
   belongs to the current series).
2. Start a `draft.ipynb` (prose-first) or a titled notebook (runnable tutorial).
3. Write in markdown cells following the style guide below.
4. Put images in `resources/` inside the article folder.
5. If the article demonstrates runnable code, add a pinned `requirements.txt` in the same folder.
6. Once published, rename the draft to the article title and add an entry to the root `README.md`
   with the title, italicised tagline, and Medium link.

### Running the tutorial notebooks

There is no repo-wide environment. Each article pins its own dependencies, and versions conflict
across articles (`networkx` alone spans 2.8.8 → 3.2.1). Create a fresh environment per article:

```bash
cd "The New Best Python Package for Visualising Network Graphs"
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

The Graph DB article additionally needs Memgraph running locally:

```bash
cd Enhance*/memgraph-platform && docker compose up -d
# Memgraph on bolt://localhost:7687, Memgraph Lab UI on http://localhost:3000
```

The Two Best Tools article was built with conda (`environment.yml`, env name `graph-comparison`);
its `prefix:` line points at the author's Windows miniconda path and should be ignored or removed
if the env is recreated.

### Verification

There are no tests to run. "Correct" means:

- Code cells in runnable articles execute top to bottom in the article's own environment.
- Committed outputs match what the prose claims they show.
- Prose matches the style guide below.

Don't add a test suite, linter config, or CI workflow unless explicitly asked — they're not part
of how this repo works.

### Git conventions

- `main` is the default branch. Commit messages are short, lowercase, and imperative
  (`add requirements`, `update readme`, `add final draft`). Match that register; don't
  over-engineer messages for a prose commit.
- Commit generated artefacts that the article depends on (notebook outputs, `Plots/*.html`,
  images in `resources/`). `.gitignore` excludes torch datasets (`/*/data/*`) and checkpoints
  (`*.pt`) — these are regenerable and large.

### Spec-driven articles

`spec driven development/` introduces a newer, deliberate workflow that is worth reusing for
substantial pieces: **write the spec before the draft.**

- `spec/GOAL.md` holds the article's brief: focus, target audience, the reaction the first
  paragraph should provoke, research on what's already been published, an explicit list of gaps
  in the existing literature, and the proposed niche this article occupies.
- `draft.md` holds the article itself, written against that brief.

When working on an article that has a `spec/` directory, **read `GOAL.md` first** and write to
the niche it defines. Don't cover ground the spec explicitly identifies as saturated. If the
article's angle changes during drafting, update `GOAL.md` to match — the spec is a living
document, not a one-shot prompt.

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
- State hardware or environment concretely when it matters to the result — the voice assistant
  article lists device specs (Macbook Air, M3, 16GB) before benchmarking local models.
- End with a reference to future articles in the series when relevant.

### Code & Technical Content
- Embed code as **fenced Python/bash code blocks** in markdown cells.
- Accompany every significant code block with a brief plain-English explanation —
  before *and/or* after the code, never just dump code alone.
- When introducing a class or function for the first time, show a **skeleton/stub version**
  first, then fill in the details progressively.
- Use install commands in their own bash code block when setting up a library.
- Name specific tools, versions, and libraries. Be concrete.
- Explicitly discuss **why** a design decision was made, not just what it is.

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

- **Network graph visualisation** (NetworkX, gravis, pyvis, ipysigma, graph databases like
  Memgraph and Kuzu)
- **LLM Agents & AI tooling** (LangGraph, MCP servers, Ollama, local LLMs)
- **Software engineering for data scientists** (code smells, design patterns, abstraction)
- **Practical Python tooling** (comparisons of libraries, step-by-step tutorials)
- **Voice assistants / AI applications** (speech-to-text, TTS, local AI pipelines)
- **AI-assisted development practice** (spec-driven development, working with coding agents)

Articles are usually **tutorial-driven** or **problem to solution** in structure. They solve
a real, relatable problem the author personally encountered.

Recent articles are written as **series**. The coding-concepts piece is explicitly "one out of a
series"; the mobile app draft opens by referring back to the voice assistant article. When
drafting, check whether the piece belongs to an existing thread and link it accordingly.

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
- One idea per markdown cell. Cells are short — a heading and its immediate prose, then a new
  cell. Don't write one giant cell containing the whole article.
- Code cells contain the actual runnable Python code demonstrated in the article — but only in
  the runnable tutorial articles. Prose-first drafts keep code in fenced blocks inside markdown.
- Keep notebook outputs for code cells that produce visualisations or useful terminal output —
  these appear inline when rendered on Medium.
- Image resources live in a `resources/` subdirectory within the article folder.
  Reference them as `![image](resources/filename.png)` in markdown cells.
- Prefer editing notebooks with the notebook editing tool over hand-patching JSON — it keeps the
  cell structure and metadata valid.

---

## Things to Avoid

- **No fluff introductions.** Don't open with "In today's rapidly evolving world of AI..."
- **No over-hedging.** Say things clearly. Don't qualify every sentence into meaninglessness.
- **No passive voice unless natural.** Prefer "I built X" over "X was built".
- **No American spellings.** (e.g. "optimize" -> "optimise", "behavior" -> "behaviour")
  Exception: existing folder names and published URLs — leave those alone.
- **No generic conclusions.** Don't end with "I hope you found this article useful!"
- **Don't explain the obvious.** Assume the reader is technical and intelligent.
- **Don't start with bullet points.** Ground the reader in narrative prose first.
- **Don't strip notebook outputs** from the runnable tutorial articles — they're part of the
  published content.
- **Don't restructure the repo** into a package layout, add tooling config, or "fix" the folder
  naming. The structure is deliberate and tied to published article URLs.
