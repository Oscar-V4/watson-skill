<p align="center">
  <img src="../assets/watson-logo.png" alt="Watson logo" width="168">
</p>

# Watson

<p align="center">
  <a href="../README.md">한국어</a> |
  <a href="README.en.md">English</a> |
  <b>简体中文</b>
</p>

**帮帮我，Watson...!**

**Watson 是一个自适应研究伙伴，会和你一起设计符合目标的执行策略。**  
它会读取用户的目标、限制条件和当前工作上下文，寻找并比较工具、GitHub 仓库、技能、MCP、SaaS/API 和工作流栈，然后整理成“可以马上使用的程序推荐”或“分层 harness 设计”。

- 读取目标和需求，并分析用户真正需要的功能。
- 搜索 GitHub、官方文档、starred repos、本地技能、MCP 和 SaaS/API 候选。
- 过滤过时仓库、维护信号弱的项目、过大的安装表面和安全风险。
- 判断 1-3 个工具是否足够，还是需要多层工作栈。
- 同时给出采用顺序、难度、风险程度、现在要做的事和可以推迟的事。

## 快速安装

把下面这段提示词直接复制给 Codex、Claude Code、Antigravity 或其他 Agent 即可。

```text
请查看这个 GitHub repo 并安装 Watson agent skill:
https://github.com/Oscar-V4/watson-skill

请检测你当前运行的 agent 环境并完成安装。
- 如果是 Codex，请安装到 ~/.codex/skills/watson。
- 如果是 Claude Code，请安装到 ~/.claude/skills/watson。
- 如果是其他 agent，请确认它是否支持基于 SKILL.md 的 skill 文件夹，并安装到最接近的用户级 skill 目录。
- 如果有专用安装器，请使用它；否则 clone 这个 repo，并把 skills/watson 文件夹复制到用户 skill 目录。

安装后，请阅读 skills/watson/SKILL.md 和 README.md，然后简短说明：
1. 什么时候应该使用 $watson
2. 应该怎样描述请求
3. 三个适合第一次测试的提示词
```

直接安装：

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo Oscar-V4/watson-skill \
  --path skills/watson
```

安装后重启你的 agent 应用，然后用 `$watson` 调用。

## 什么时候使用

| 场景 | 可以这样说 |
|---|---|
| 不知道该用什么工具 | `$watson 帮我寻找并比较这个任务适合的 GitHub repo、MCP 和 SaaS/API 候选。` |
| 想反映自己的偏好或收藏列表 | `$watson 也看看我的 GitHub stars，并推荐适合这个项目的工具栈。` |
| 不确定单一工具是否足够 | `$watson 判断这个任务用单一 API 就够了，还是需要分层 harness。` |
| 想设计 Agent 工作流 | `$watson 设计一个包含研究、实现、验证和记忆的 agentic workflow。` |
| frontend/AI 工具太多太乱 | `$watson 从最新 frontend AI 工具里只筛选仍在维护的选项。` |
| 安装前想看风险 | `$watson 请为每个候选补充安装难度、权限表面和安全/信任风险。` |

## 输出形式

Watson 通常会这样回答：

- **Task Read**：用户目标和所需能力的摘要
- **Expert Lenses**：本次探索使用的 1-3 个专家 persona
- **Discovery Summary**：从 GitHub、stars、web/SaaS/API、本地 skills、MCP 中确认的内容
- **Candidate Table**：候选的用途、freshness、信任/安全备注、难度和时机
- **Recommended Path**：判断是简单推荐，还是分层 harness 设计
- **Do Now / Defer / Avoid**：现在做、推迟做、避免或观察的事项

## 身份定位

Watson 更接近 **设计伙伴 + 自适应策略师**。

- 像同事一样整理目标、限制、线索和风险信号。
- 根据任务性质调整研究深度和推荐方式。
- 它给出的不是“看起来不错的工具列表”，而是“现在该采用什么，以及如何采用”。

## Agent 兼容性

这个 repo 按 `SKILL.md` agent skill 结构打包。像 Codex 和 Claude Code 这样会读取用户 skill 文件夹的 agent 可以直接安装；其他 agent 也可以读取 `skills/watson/SKILL.md`，按同一套指令使用。

不同 agent 的自动加载规则可能不同。最可靠的方式是把上面的“快速安装”提示词贴给 agent，让它根据当前环境完成安装。

## 安全边界

默认情况下，Watson 只输出推荐和设计 brief。除非用户明确要求，否则它不会执行以下操作：

- 安装 package、MCP、skill 或全局设置
- 创建账号、开启免费试用或订阅付费服务
- 执行深度安全审计
- 修改项目代码

## Skill 全文

<details>
<summary><code>skills/watson/SKILL.md</code></summary>

````markdown
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
````

</details>

## 仓库结构

```text
watson-skill/
├── README.md
├── assets/
│   └── watson-logo.png
├── docs/
│   ├── README.en.md
│   └── README.zh-CN.md
└── skills/
    └── watson/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            └── pilot-validation.md
```
