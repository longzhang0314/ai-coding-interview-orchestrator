# AI Coding Interview Skills

一套用于 **AI Coding 面试 / 笔试 / Take-home 题目** 的本地 agent skill 工具包。

它把重复的面试执行流程内化到 skill 里：你只需要调用 skill，然后贴题目截图、README、需求文本或现有代码，工具会自动按下面流程推进：

```text
需求澄清 -> 业务建模 -> 极简 spec -> 实现计划 -> 人工审查 -> 编码 -> 验证 -> 交付说明
```

默认情况下，工具会在任务拆解和文件级计划完成后暂停，让你人工审查范围、优先级和修改文件。你确认后，它才会开始自动编码；如果你明确说“跳过审查”或“全自动执行”，才会直接实现。

验证失败后也有边界：默认最多执行 2 轮“修复 -> 重新验证”。如果仍不通过，工具会停止自动修复，输出受控未完成报告，避免在面试中无限循环。

## 适用场景

- AI Coding 面试或笔试
- 给一个模糊业务需求，让你现场实现
- 给一个 README，让你补全项目功能
- 给一段陌生业务代码，让你分析并实现工具
- 需要用 Codex 或 Claude Code 快速把需求转成可运行代码
- 需要最终输出面试官能看懂的交付说明

## 目录结构

```text
.
├── README.md
└── skills
    ├── codex
    │   └── ai-coding-interview-orchestrator
    │       ├── SKILL.md
    │       ├── agents
    │       │   └── openai.yaml
    │       └── references
    └── claude-code
        └── ai-coding-interview-orchestrator
            ├── SKILL.md
            └── references
```

## 快速安装

### 安装到 Codex

在仓库根目录执行：

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/ai-coding-interview-orchestrator ~/.codex/skills/
```

安装后建议新开一个 Codex 会话，让 skill 列表刷新。

使用方式：

```text
请使用 $ai-coding-interview-orchestrator。
```

然后直接贴题目截图、README、需求文本或代码。

### 安装到 Claude Code

在仓库根目录执行：

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude-code/ai-coding-interview-orchestrator ~/.claude/skills/
```

安装后建议新开一个 Claude Code 会话，让 skill 列表刷新。

使用方式：

```text
使用 ai-coding-interview-orchestrator。
```

然后直接贴题目截图、README、需求文本或代码。

## 面试时的最短启动方式

### Codex

```text
请使用 $ai-coding-interview-orchestrator。
```

### Claude Code

```text
使用 ai-coding-interview-orchestrator。
```

你不需要再重复粘贴“需求澄清、业务建模、极简 spec、实现计划、编码、验证、交付说明”等长提示词，这些已经内化到 skill 里。

默认会在实现前停下来让你审查任务拆解。确认后可以说：

```text
确认，开始实现。
```

如果这次想全自动执行，可以说：

```text
本次跳过人工审查门，直接实现并验证。
```

如果你愿意临时放宽修复次数，可以说：

```text
允许最多 4 轮修复验证。
```

## 如果想显式控制流程

可以使用完整启动语：

```text
我正在进行 AI Coding 面试/笔试。下面是题目截图、README 或现有代码。
请按需求澄清、业务建模、极简 spec、实现计划、编码、验证、交付说明的流程完成。
需求不清晰时最多问 1 个关键问题；如果我没有回答，请基于合理假设继续。
```

## 工具内置能力

- 读取题目和代码结构
- 将陌生业务抽象成通用工程模型
- 生成极简 spec
- 生成文件级实现计划
- 在实现前提供人工审查门，支持你调整任务范围和优先级
- 限制验证失败后的自动修复轮次，默认最多 2 轮
- 支持 Task / subagent 风格分工
- 支持面试压缩版流程纪律
- 提供验证清单
- 提供最终交付报告模板

## 纯提示词版多 Agent 模板

如果面试环境不允许使用预置 skill，可以直接使用 `prompts/multi-agent/` 下的纯提示词模板：

```text
prompts/multi-agent/
├── README.md
├── main-agent.md
├── subagent-requirement-context-analyst.md
├── subagent-test-reporter.md
├── subagent-repair-advisor.md
└── subagent-final-reviewer.md
```

推荐分工：

- `main-agent.md`：主 agent，负责领域模型、技术方案、人工确认、编码实现和最终交付。
- `subagent-requirement-context-analyst.md`：只读分析 README、需求和项目上下文。
- `subagent-test-reporter.md`：只读整理测试命令和测试报告。
- `subagent-repair-advisor.md`：只读分析失败原因并提出最小修复建议。
- `subagent-final-reviewer.md`：只读做交付前复核，可选。

默认不要让子 agent 直接改代码；主 agent 始终负责最终实现。

## 内置参考模板

每个版本都包含 `references/`：

- `domain-patterns.md`：陌生业务抽象套路
- `execution-flow.md`：完整执行流程
- `final-report-template.md`：最终交付说明模板
- `quick-prompts.md`：快捷提示词
- `spec-template.md`：极简 spec 模板
- `subagent-briefs.md`：Task / subagent 角色提示词
- `verification-checklist.md`：验证检查清单

## 推荐使用姿势

1. 新开 Codex 或 Claude Code 会话。
2. 进入面试题所在项目目录。
3. 调用对应 skill。
4. 粘贴题目截图、README 或需求文本。
5. 让工具先输出题目理解、关键假设、最小可交付范围、实现计划和验证方式。
6. 确认方向没问题后继续实现。

## 注意事项

- 如果新安装后没有触发，重启或新开一个会话。
- 面试限时场景优先做核心闭环，不要追求大而全架构。
- 测试失败时默认最多自动修 2 轮；超过后应让人决定继续修、降级交付还是说明风险。
- 如果依赖无法安装或测试无法运行，最终交付说明里要如实写明验证替代方式。
- 真实面试中要遵守平台规则；如果平台不允许使用 AI 工具，不要违规使用。
