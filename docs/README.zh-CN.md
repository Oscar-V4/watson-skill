# Watson

<p align="center">
  <a href="../README.md">한국어</a> |
  <a href="README.en.md">English</a> |
  <b>简体中文</b>
</p>

**Watson 是一个自适应研究伙伴，用来为目标结果设计合适的执行路径。**  
它会读取你的目标、限制条件和当前工作上下文，然后比较工具、GitHub 仓库、技能、MCP、SaaS/API 和工作流栈，最后给出简单工具推荐或分层 harness 设计。

- 把目标拆成真正需要的能力。
- 搜索 GitHub、官方文档、starred repos、本地技能、MCP 和 SaaS/API。
- 过滤过时仓库、维护信号弱的项目、安装成本过高的方案和明显信任风险。
- 判断 1-3 个工具是否足够，还是需要多层工作流栈。
- 给出采用顺序、难度、风险说明，以及现在做什么、以后再看什么。

## 快速安装

把下面这段提示词复制给 Codex、Claude Code、Antigravity 或其他编码 Agent，它就可以按当前环境安装并说明如何使用。

```text
请查看这个 GitHub 仓库并安装 Watson agent skill:
https://github.com/Oscar-V4/watson-skill

请检测你当前运行的 agent 环境。
- 如果是 Codex，请安装到 ~/.codex/skills/watson。
- 如果是 Claude Code，请安装到 ~/.claude/skills/watson。
- 如果是其他 agent，请确认它是否支持基于 SKILL.md 的 skill 文件夹，并安装到最接近的用户级 skill 目录。
- 如果有内置 skill installer，请优先使用；否则 clone 这个 repo，并把 skills/watson 复制到用户 skill 目录。

安装后，请阅读 skills/watson/SKILL.md 和 README.md，然后告诉我：
1. 什么时候应该使用 $watson
2. 应该怎样描述请求
3. 三个适合第一次测试的提示词
```

Codex 直接安装：

```bash
python ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo Oscar-V4/watson-skill \
  --path skills/watson
```

安装后重启你的 agent 应用，然后用 `$watson` 调用。

## 什么时候使用

| 场景 | 可以这样说 |
|---|---|
| 不知道该用哪些工具 | `$watson 帮我比较这个任务适合的 GitHub repos、MCP 和 SaaS/API 候选。` |
| 想结合自己的收藏偏好 | `$watson 如果可以，请查看我的 GitHub stars，并推荐这个项目的工具栈。` |
| 不确定单一工具是否足够 | `$watson 判断这个任务用单一 API 就够了，还是需要分层 harness。` |
| 需要设计 Agent 工作流 | `$watson 设计一个包含研究、实现、验证和记忆的 agentic workflow。` |
| AI/frontend 工具太多太乱 | `$watson 只筛选仍在维护的 frontend AI 工具，并降低过时 repo 的优先级。` |
| 安装前想看风险 | `$watson 请为每个候选补充安装难度、权限表面和信任/安全风险。` |

## 输出形式

Watson 通常会返回：

- **Task Read**：目标和缺失的能力
- **Expert Lenses**：本次搜索使用的 1-3 个视角
- **Discovery Summary**：检查过的 GitHub、stars、web/SaaS/API、本地 skills 和 MCP
- **Candidate Table**：用途、freshness、信任/安全备注、难度和采用时机
- **Recommended Path**：简单推荐或分层 harness
- **Do Now / Defer / Avoid**：现在做、以后看、避免或观察的事项

## 兼容性

这个仓库按 `SKILL.md` agent skill 结构打包。Codex 和 Claude Code 这类支持用户 skill 目录的 agent 可以直接安装；其他 agent 也可以通过读取 `skills/watson/SKILL.md` 使用同一套指令，但自动发现规则会因产品而异。

## 默认边界

Watson 默认只输出推荐和设计 brief。除非用户明确要求，它不会安装工具、创建账号、开启付费试用、执行深度安全审计或修改项目代码。
