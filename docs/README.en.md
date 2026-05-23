# Watson

<p align="center">
  <a href="../README.md">한국어</a> |
  <b>English</b> |
  <a href="README.zh-CN.md">简体中文</a>
</p>

**Watson is an adaptive research partner for designing the right path to a target result.**  
It reads your goal, constraints, and current work context, then compares tools, GitHub repos, skills, MCPs, SaaS/APIs, and workflow stacks before recommending either a simple tool path or a layered harness.

- Breaks a goal into the capabilities it actually needs.
- Searches GitHub, official docs, starred repos, local skills, MCPs, and SaaS/API options.
- Filters stale repos, weak maintenance signals, high-friction setup, and obvious trust risks.
- Decides whether one to three tools are enough or a layered workflow stack is warranted.
- Reports adoption order, difficulty, caveats, and what to do now versus later.

## Quick Install

Share this prompt with a friend. They can paste it into Codex, Claude Code, Antigravity, or another coding agent and let the agent install the skill.

```text
Please inspect this GitHub repo and install the Watson agent skill:
https://github.com/Oscar-V4/watson-skill

Detect the agent environment you are running in.
- If this is Codex, install it into ~/.codex/skills/watson.
- If this is Claude Code, install it into ~/.claude/skills/watson.
- If this is another agent, check whether it supports SKILL.md-based skill folders and install it in the closest user-level skill location.
- Use a built-in skill installer if available; otherwise clone the repo and copy skills/watson into the user skill directory.

After installation, read skills/watson/SKILL.md and README.md, then explain:
1. when I should use $watson
2. how I should phrase requests
3. three starter prompts to test it
```

Direct Codex install:

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo Oscar-V4/watson-skill \
  --path skills/watson
```

Restart your agent app after installation, then invoke the skill with `$watson`.

## When To Use It

| Situation | Say this |
|---|---|
| You do not know which tools to use | `$watson Find and compare GitHub repos, MCPs, and SaaS/API options for this task.` |
| You want your existing taste reflected | `$watson Inspect my GitHub stars if available and recommend a tool stack for this project.` |
| You are unsure whether one tool is enough | `$watson Decide whether this should use one API or a layered harness.` |
| You need an agent workflow | `$watson Design an agentic workflow covering research, implementation, verification, and memory.` |
| The AI/frontend tooling space feels noisy | `$watson Filter for maintained frontend AI tools and downgrade stale repos.` |
| You want adoption risk called out | `$watson Include setup difficulty, permission surface, and trust/security caveats for each candidate.` |

## Output Shape

Watson usually returns:

- **Task Read**: the goal and missing capability classes
- **Expert Lenses**: 1-3 perspectives for the search
- **Discovery Summary**: GitHub, stars, web/SaaS/API, local skills, and MCPs checked
- **Candidate Table**: use, freshness, trust/security note, difficulty, and timing
- **Recommended Path**: simple recommendation or layered harness
- **Do Now / Defer / Avoid**: immediate actions and things to skip or watch

## Compatibility

This repo is packaged as a `SKILL.md`-based agent skill. Agents such as Codex and Claude Code can install it as a user skill. Other agents can still use it by reading `skills/watson/SKILL.md`, though automatic skill discovery rules vary by product.

## Default Boundary

Watson produces recommendations and design briefs by default. It does not install tools, create accounts, start paid trials, perform deep security audits, or modify project code unless the user explicitly asks for that action.
