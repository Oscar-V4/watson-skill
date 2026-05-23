# Pilot Validation

Use this reference only when testing or revising `watson`.

## Original Intent Prompt

The user's condensed Korean planning prompt can be summarized as:

> Act as a creative, world-class LLM/AI/agentic engineering/development expert such as an Andrej Karpathy-like researcher, Garry Tan-like founder-engineer, or a brilliant agentic engineering competition winner. Understand my prompt, plan, requirements, situation, current work, and harness context. Search GitHub broadly and creatively for helpful skills, programs, stacks, and tools; inspect my starred repositories because I often star trending or useful repos. Recommend candidates with a light security check plus simple difficulty and constraint notes so I can judge whether each is immediately usable or should be deferred. Also search beyond GitHub for useful SaaS, API integrations, paid services, or programs that could be substitutes or linchpins. If the task only needs one or a few tools, recommend those and stop. If it needs a complex layered harness, synthesize that harness.

## First Pilot Scenario

Use this prompt for the first practical validation:

> Assume a blank workspace. Based on the purpose of a design-oriented website-cloning workspace, virtually design a harness for website design format and information extraction plus a Claude Design-like exceptional design/frontend skill setup. Search GitHub broadly, include relevant skill banks and starred repositories if available, consider non-GitHub SaaS/API/tools, lightly assess security and setup difficulty, and recommend either a few simple tools or a layered harness.

Expected behavior:

- Do not install anything.
- Do not sign up for paid tools.
- Do not implement code.
- Use current GitHub/web research.
- Include a freshness check for GitHub candidates and downgrade/exclude stale AI/agentic/frontend repos unless there is a strong stability exception.
- Try to inspect GitHub stars; if unavailable, say why.
- Likely produce a layered harness because the pilot combines extraction, design skill/persona, frontend implementation support, and verification.
- Preserve a short list of immediate low-friction tools versus heavier future investments.

## Feedback Rubric

Ask the user to judge:

- Did the result feel like a high-level expert reframed the problem, not just a search dump?
- Were candidates surprising or useful enough to change the harness?
- Were setup difficulty and constraints clear enough to make decisions?
- Were security/trust notes honest without pretending to be a full audit?
- Did the result avoid stale repos unless it gave a strong exception?
- Did it choose the right ending: simple recommendation or layered harness?
- Did it respect default permission boundaries?
