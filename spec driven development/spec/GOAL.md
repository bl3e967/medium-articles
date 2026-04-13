# GOAL

Article focus: Provide a personal example of how I structured my spec driven development process to achieve a high quality product and engineering workflow.

Target audience:
Other engineers who are interested in spec driven development and who want to read real life examples to get inspiration from and learn from other people's work.

The article should be written in a way that is easy to read and understand. 

Within the first paragraph, a reader should think "that's interesting. This approach is unique, and I want to learn more about it."

## Existing article research

### What's already saturated

The existing content splits into four clear buckets:

**1. Definition/overview articles** — "What is SDD, why it matters, the three levels (spec-first, spec-anchored, spec-as-source)." Covered thoroughly by Thoughtworks, Augment Code, Martin Fowler, multiple Medium posts. Nobody needs another one.

**2. Tool tutorials** — "How to use SDD with Claude Code / GitHub spec-kit / Kiro / Cursor." Step-by-step guides with scaffolded commands. Already well covered ([alexop.dev](https://alexop.dev/posts/spec-driven-development-claude-code-in-action/), [heeki.medium.com](https://heeki.medium.com/using-spec-driven-development-with-claude-code-4a1ebe5d9f29), [cc-sdd GitHub](https://github.com/gotalab/cc-sdd)).

**3. Complex infra walkthroughs** — AWS Bedrock interceptors, Nuxt storage layer migrations, multi-file refactors with subagent delegation. Technical but niche, and mostly backend/cloud engineering.

**4. Critique / counter-arguments** — "SDD is waterfall in markdown," limits at scale, SDD failing in practice (33 mins + 2,577 markdown lines for 689 lines of code). The failure-mode angle is surprisingly well covered ([dev.to](https://dev.to/casamia918/why-spec-driven-development-fails-and-what-we-can-learn-from-it-2pec), [isoform.ai](https://isoform.ai/blog/the-limits-of-spec-driven-development), [Prezi Engineering](https://engineering.prezi.com/we-tried-spec-driven-development-so-you-dont-have-to-56d52231c19e)).

---

### The gaps — where there's room

**Gap 1: Nobody shows the spec evolving.**
Every article says "iterate on the spec" but nobody actually shows it. No before/after of a spec at v1 (vague, ambitious), v2 (interrogated, tightened), v3 (implementation-ready). The *process* of writing a good spec is invisible in the literature.

**Gap 2: The individual contributor / data scientist perspective is absent.**
Virtually all existing articles are written from a backend engineer or enterprise team angle. Nobody has written about what SDD looks like for a solo Python developer or data scientist building personal tools — where there's no team to coordinate with, no product manager, and the "spec" is essentially a conversation with yourself.

**Gap 3: Quality as the goal, not productivity.**
The dominant framing is productivity: "SDD is faster than vibe coding." But the more interesting claim — and the harder one to substantiate — is that SDD produces *better software*. Higher coherence, fewer architectural U-turns, cleaner separation of concerns. This angle is almost entirely absent.

**Gap 4: What the spec writing process reveals about your own unclear thinking.**
Nobody talks about the meta-value of SDD: that forcing yourself to write a spec exposes the things you don't actually know about what you want to build. The spec is as much a diagnostic tool as a communication tool.

**Gap 5: The spec as a durable design document, not a one-shot prompt.**
The "spec-anchored" level (keep the spec alive as the project evolves) is mentioned in theory but no article shows what this actually looks like across a real project lifecycle — updating the spec as requirements shift, using it to re-orient after a break.

---

### Proposed niche for this article

**The spec as a thinking tool — a personal walkthrough showing the actual evolution of a real project's spec, from vague idea to coherent implementation.**

The hook that makes this different:
- Written from an individual data scientist / Python developer perspective (not enterprise, not backend infra)
- Shows the *actual spec* at multiple stages — raw v1 draft, refined v2 after self-interrogation, final v3 used for implementation
- Focuses on quality and coherence as the payoff, not just speed
- Honest about the friction: what's annoyingly slow, where the process almost collapsed
- The central claim: writing the spec taught me more about what I wanted to build than the building itself did

This sits in the gap between the "here's how to use the tool" articles and the abstract "SDD changes everything" think-pieces. It's the personal, reflective, show-your-work piece that doesn't exist yet.