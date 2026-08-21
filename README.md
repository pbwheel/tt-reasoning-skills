# tt-reasoning-skills

13 个可组合的推理 skill，让 AI agent 在动手之前先想清楚。

[English](README.en.md) · [简体中文](README.md)

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Harness](https://img.shields.io/badge/Claude%20Code%20%C2%B7%20Codex%20%C2%B7%20Cursor-supported-1f6feb)

> 范围说明：这是一套**推理方法论** skill 库——帮 agent 诊断「什么在阻碍进展」并选对思考路径。它不是代码生成工具，不替代领域专业知识，也不承诺一次给出「完美答案」。

## 它解决什么问题

Agent 直接给答案时，最常见的失败不是知识不够，而是卡在六类认知缺口之一：问题本身没问清、机制没吃透、证据不足、方案被惯性假设束缚、决策依据脆弱、或方向本身不明。本库把 12 个经典推理方法做成职责单一的原子 skill，再加一个 `reason` 路由器负责诊断与调度：

```text
                         reason
                            |
              +-------------+-------------+
              v             v             v
          Understand      Research        Solve
              |             |             |
              +-------------+-------------+
                            v
                          Decide
                            |
                            v
                         Validate
```

| 认知缺口 | 对应 skill |
|---|---|
| Clarity · 清晰度 | `socratic-clarify` |
| Knowledge · 理解 | `explain-two-levels`, `reverse-engineer` |
| Evidence · 证据 | `deep-research`, `fact-audit` |
| Solution · 方案 | `first-principles`, `cross-domain`, `expert-panel` |
| Decision · 决策 | `steelman-decision`, `minimum-experiment` |
| Direction · 方向 | `talent-discovery`, `life-design` |

当请求的交付物没有被任何认知缺口阻塞时，`reason` 直接完成任务，不强行套用推理流程。

## 核心特性

- **reason 路由器**：先诊断最高的阻塞缺口，再选择最短足够路径；没有缺口就直接干活，不强加推理流程
- **可组合成链**：skill 按依赖组合（如 `first-principles -> steelman-decision -> minimum-experiment`），每完成一步重新评估，用户能采取下一个有意义的行动即停
- **共享协议**：证据、提问、组合与边界行为由 5 份 protocol 统一约束，13 个 skill 行为一致、可互换
- **平台无关**：纯 Markdown，无脚本、无依赖

## 安装

### 方式一：npx skills（推荐）

```bash
# 安装到当前项目（自动识别你的 agent）
npx skills add pbwheel/tt-reasoning-skills

# 或全局安装，对所有项目生效
npx skills add pbwheel/tt-reasoning-skills -g

# 先看看仓库里有什么
npx skills add pbwheel/tt-reasoning-skills --list
```

安装位置：Claude Code 写入 `.claude/skills/`，Cursor / Codex 类写入 `.agents/skills/`（加 `-g` 为用户级 `~/` 安装）。

注意：`skills` CLI 只复制各 skill 目录，而 `reason` 路由器依赖仓库根的 `protocols/`（经 `../..` 相对路径引用）。npx 安装后请把 `protocols/` 一并复制到与 `skills/` 同级的目录（如 `.claude/protocols/`）。

### 方式二：手动复制

把仓库里的 `skills/` 和 `protocols/` 两个目录复制到同一父目录下，例如 `.claude/skills/` 与 `.claude/protocols/`。`reason` 路由器通过 `../..` 相对路径引用 protocols，两个目录必须保持并排结构。

### 方式三：把仓库 URL 丢给 agent

直接把下面这句话发给 agent，让它自己读取并路由：

> Read https://github.com/pbwheel/tt-reasoning-skills and follow its `skills/reason/SKILL.md` to route this question through the right reasoning skills: 「……」

## 技能目录

| 类别 | Skill | 一句话职责 |
|---|---|---|
| Router | [`reason`](skills/reason/SKILL.md) | 诊断缺口，选择并执行最短足够推理路径 |
| Clarify | [`socratic-clarify`](skills/socratic-clarify/SKILL.md) | 把模糊混杂的问题变成可行动的问题定义 |
| Learn | [`explain-two-levels`](skills/explain-two-levels/SKILL.md) | 先直觉模型后专业机制地吃透一个概念 |
| Learn | [`reverse-engineer`](skills/reverse-engineer/SKILL.md) | 从成功作品反推问题、原则与可迁移经验 |
| Research | [`deep-research`](skills/deep-research/SKILL.md) | 建立带来源支撑的主题全景：历史、现状、走向 |
| Research | [`fact-audit`](skills/fact-audit/SKILL.md) | 核验事实，并检验事实是否真能支撑结论 |
| Solve | [`first-principles`](skills/first-principles/SKILL.md) | 剥离惯性假设，从事实与目标重新推导方案 |
| Solve | [`cross-domain`](skills/cross-domain/SKILL.md) | 在远域同构问题中找成熟机制，再带边界迁移回来 |
| Solve | [`expert-panel`](skills/expert-panel/SKILL.md) | 用真正互补的专业模型分析，暴露分歧后综合 |
| Decide | [`steelman-decision`](skills/steelman-decision/SKILL.md) | 给每个选项造最强论证后，再做有据选择 |
| Decide | [`minimum-experiment`](skills/minimum-experiment/SKILL.md) | 把关键不确定性变成最便宜的可反转实验 |
| Self | [`talent-discovery`](skills/talent-discovery/SKILL.md) | 从经历证据推断可迁移优势及其触发条件 |
| Self | [`life-design`](skills/life-design/SKILL.md) | 从现状与价值观生成多条可检验的未来路径 |

## 工作原理

路由与行为由共享协议约束（位于 [`protocols/`](protocols/)）：

- [`reasoning-contract.md`](protocols/reasoning-contract.md)：所有 skill 的公共契约（元数据、行为要求、缺口分类）
- [`evidence-policy.md`](protocols/evidence-policy.md)：区分事实、推断、假设、判断与未知
- [`questioning-policy.md`](protocols/questioning-policy.md)：约束 skill 何时可以停下来提问
- [`composition-policy.md`](protocols/composition-policy.md)：定义合法组合路径与禁止组合
- [`skill-boundaries.md`](protocols/skill-boundaries.md)：路由与边界的唯一事实来源

`reason` 读取边界与组合规则 → 诊断最高阻塞缺口 → 选择一个 skill 或一条链 → 执行并在每步后重评。调用方式取决于你的 agent：Claude Code 会根据 description 自动触发，也可以直接说「用 fact-audit 核验这个说法」；Codex 类 agent 可用 `$reason` 这样的命令语法；plan-only 模式只输出路由结果不执行。

## 使用示例

- **工程决策**：「Should we rewrite our legacy service in Rust?」→ 路由为 `first-principles -> steelman-decision -> minimum-experiment`，任一步使你能够行动即提前停止
- **个人发展**：从一段具体经历出发，`talent-discovery` 推断可迁移优势，`life-design` 生成多条可检验的未来路径，必要时以 `minimum-experiment` 收尾

完整工作流见 [`examples/`](examples/)（软件工程 / 产品决策 / 研究 / 个人发展四类），路由行为用例见 [`evals/`](evals/)。

## 边界（非目标）

- 不替代领域专业知识：skill 组织推理过程，专业内容仍需领域输入
- 不生成代码、不执行工程动作：这是推理方法库
- 不追求一次给出「完美答案」：每一步以「用户能采取下一个有意义的行动」为停止条件
- 不承诺实时联网检索：`deep-research` 与 `fact-audit` 在宿主 agent 的工具能力范围内工作

## License

[MIT](LICENSE) · Copyright (c) 2026 pbwheel
