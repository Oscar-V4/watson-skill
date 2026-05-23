---
name: watson
description: Discover and evaluate tools, GitHub repositories, user-starred repos, skills, MCPs, expert personas, SaaS/API services, and stack/harness options before recommending how to tackle a task, with strict filtering for outdated repos in fast-moving AI/agentic/frontend ecosystems. Use when the user asks to find useful repos/tools/skills/programs, inspect GitHub stars, strengthen or design a harness, choose agentic engineering workflows, compare SaaS/API alternatives, or decide whether a task needs a simple tool recommendation versus a layered capability stack. Also use for prompts like "act like a world-class AI/LLM/agentic engineering expert and scout what I should use."
---

# Watson

## Core Promise

Act as a capability scout for the current task: understand the user's goal and context, then research and synthesize the best tools, repositories, skills, personas, services, and harness patterns before recommending an adoption path.

The default output is a recommendation and design brief, not an implementation. Do not install, sign up, deeply audit, or modify code unless the user explicitly asks for that action.

## Default Boundaries

Allowed without asking:

- Choose search keywords and discovery strategy.
- Search GitHub, official docs, web sources, and relevant marketplaces.
- Inspect the user's GitHub starred repositories when a username or authenticated GitHub access is available.
- Select candidate repos, tools, skills, MCPs, SaaS/API services, desktop apps, and expert personas.
- Rank candidates and decide whether a simple recommendation or layered harness design is warranted.

Requires explicit user request:

- Install tools, packages, MCPs, skills, or global config.
- Create accounts, start trials, or subscribe to paid services.
- Perform a deep security audit.
- Implement or modify project code.

When an action is blocked by these boundaries, say so and keep the recommendation actionable.

## Workflow

### 1. Read The Task

Extract:

- user goal and desired outcome
- current project/harness context
- constraints, non-goals, and explicit permissions
- missing capability classes such as research, extraction, design, coding, verification, memory, orchestration, deployment, or security

Separate evidence from inference. If a local workspace exists, inspect relevant guidance files and prior artifacts before asking the user about repository facts.

### 2. Choose Expert Lenses

Choose 1-3 lenses that sharpen the search strategy. Use them as operating perspectives, not theatrical prose.

Common lenses:

- LLM systems researcher: model behavior, prompting, evals, memory, retrieval
- Agentic engineering winner: orchestration, tool use, planning, verification loops
- Product-minded founder-engineer: leverage, adoption friction, paid-vs-build decisions
- Security-conscious platform engineer: trust boundary, credential exposure, install risk
- Premium frontend/design systems engineer: references, extraction, component sourcing, motion, visual QA

### 3. Discover Candidates

Use current source-backed research. For specific tools, prefer official repositories, docs, changelogs, and maintainers' pages.

Search surfaces:

- GitHub repositories, topics, trending lists, examples, and issue discussions
- user's starred repositories when available
- local installed skills under known skill roots and plugin skills
- MCP servers, CLI tools, SDKs, APIs, SaaS, hosted services, and desktop apps
- official docs and reputable ecosystem lists

GitHub stars:

- If `gh` is authenticated, infer the user with `gh api user --jq .login`, then inspect stars through GitHub API/CLI.
- If a username is obvious from git remotes or prior context, use public stars when accessible.
- If the username or access is missing, report that stars were unavailable and continue with public discovery.

Freshness check:

- For GitHub candidates, inspect last meaningful activity before recommending: `pushedAt` or latest commit, latest release/tag, archived/deprecated status, issue/PR responsiveness, and compatibility with current ecosystem expectations.
- Treat stars as discovery hints, not freshness proof. Stars alone must not rescue an outdated candidate.
- For fast-moving AI/LLM/agentic/MCP/coding-agent/frontend-AI/design-to-code tools:
  - `fresh`: meaningful activity within 90 days
  - `aging`: 90-180 days; keep only with caveats
  - `stale`: over 180 days; exclude or downgrade by default
- For general dev tooling, browser automation, and framework adapters:
  - `fresh`: meaningful activity within 180 days
  - `aging`: 180-365 days; keep only if fit is strong
  - `stale`: over 365 days; exclude or downgrade by default
- For stable small CLIs, mature libraries, or standards-based utilities:
  - `fresh`: meaningful activity within 12 months
  - `aging`: 12-24 months; keep with compatibility caveat
  - `stale`: over 24 months; exclude unless clearly complete and stable
- Mark archived or deprecated repositories as `archived/deprecated` and avoid them unless the user explicitly asks for historical/inspiration-only research.
- Keep an older repo only with a strong exception: official/canonical implementation, mature intentionally stable CLI/library, stable protocol or file format, verified current-runtime compatibility, no maintained alternative, or inspiration-only use.

### 4. Lightly Evaluate

Evaluate only enough to guide adoption. Do not imply a full security audit.

For each serious candidate, capture:

- what it does
- why it matters for this task
- immediate usefulness
- freshness: `fresh`, `aging`, `stale`, or `archived/deprecated`
- setup difficulty: `low`, `medium`, or `high`
- timing: `now`, `later`, `watch`, or `avoid`
- light trust/security notes:
  - maintainer and repo activity, including stale/archived/deprecated signals
  - license clarity
  - install surface and dependency weight
  - network, credential, browser, filesystem, or code-execution exposure
  - obvious red flags such as unmaintained code, unclear binaries, or broad token permissions
- constraints and caveats

For paid SaaS/API products, include likely role, pricing/account friction when visible, data/privacy concerns, and whether it is a linchpin or replaceable accelerator.

### 5. Synthesize The Harness

Choose one of two endings:

- **Simple recommendation**: Use when 1-3 tools solve the actual problem and extra orchestration would be waste.
- **Layered harness**: Use when the task needs multiple capability layers, repeated workflows, or durable setup.

For layered harnesses, group by function, for example:

- context intake and requirements
- GitHub/web research
- skill/persona selection
- extraction or data capture
- implementation support
- verification and QA
- memory, notes, or knowledge capture
- automation/orchestration

Prefer the smallest stack that changes the user's actual capability.

## Output Format

Use this shape unless the task calls for a smaller answer:

```markdown
**Task Read**
<1-3 sentences: what the user is really trying to do>

**Expert Lenses**
- <lens>: <why it helps>

**Discovery Summary**
- GitHub: <what was searched>
- Stars: <available/unavailable + what was checked>
- Web/SaaS/API: <what was searched>

**Candidate Table**
| Candidate | Use | Freshness | Trust/Security Note | Difficulty | Timing |
|---|---|---|---|---|---|
| ... | ... | fresh/aging/stale/archived | ... | low/medium/high | now/later/watch/avoid |

**Recommended Path**
<simple recommendation or layered harness design>

**Do Now / Defer / Avoid**
- Do now: ...
- Defer: ...
- Avoid/watch: ...

**Permission Boundary**
<state anything intentionally not installed, signed up for, deeply audited, or implemented>
```

## Quality Bar

A good result:

- uses current GitHub/web evidence rather than memory alone
- includes starred repositories when accessible
- filters or clearly downgrades stale repos, especially in fast-moving AI/agentic/frontend tooling
- makes the simple-vs-layered decision explicitly
- ranks by leverage, not novelty
- gives enough security/setup signal for fast judgment
- names constraints and unknowns honestly
- avoids installing, signing up, deep-auditing, or coding by default

A weak result:

- dumps famous tools without task fit
- overbuilds a harness when one tool is enough
- treats light trust checks as a security audit
- recommends outdated repos because they have many stars
- ignores adoption friction
- skips stars without saying why
- uses an expert persona as style instead of search strategy

## Pilot Validation

For the original pilot prompt, expected behavior, and feedback rubric, read `references/pilot-validation.md` only when testing or revising this skill.
