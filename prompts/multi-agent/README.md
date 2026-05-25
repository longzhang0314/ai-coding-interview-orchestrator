# Multi-Agent Prompt Set

这是一套 **不依赖 skill 的纯提示词版多 agent 工作流**。

适用场景：面试官允许使用 AI 工具，但不允许使用预置 skill；或者你想手动控制主 agent 和子 agent 的分工。

## 推荐架构

```text
Main Agent
  ├── Requirement Context Analyst  只读：README / 需求 / 项目结构分析
  ├── Test Reporter                只读：测试命令、测试结果、失败摘要
  ├── Repair Advisor               只读：修复建议、最小改动方案
  └── Final Reviewer               只读：最终交付前复核，可选
```

## 核心原则

- 主 agent 始终是 tech lead，负责领域模型、方案设计、任务拆解、人工确认、编码实现和最终交付。
- 子 agent 默认只读，不直接修改文件。
- 子 agent 只产出结论、风险和建议，不做开放式探索。
- 不要让多个子 agent 同时改代码。
- 时间紧张时只用 `Requirement Context Analyst` 和 `Test Reporter`。
- 复杂或失败场景再使用 `Repair Advisor`。
- 最终交付前有时间再使用 `Final Reviewer`。

## 文件说明

- `main-agent.md`：主 agent 提示词，负责全流程和代码实现。
- `subagent-requirement-context-analyst.md`：需求和 README 分析子 agent。
- `subagent-test-reporter.md`：测试执行和测试报告子 agent。
- `subagent-repair-advisor.md`：失败原因分析和修复建议子 agent。
- `subagent-final-reviewer.md`：最终交付前复核子 agent。

## Claude Code 安装方式

如果要让 Claude Code 直接识别这些子 agent，可以复制到用户级 agents 目录：

```bash
mkdir -p ~/.claude/agents
cp prompts/multi-agent/subagent-*.md ~/.claude/agents/
```

也可以复制到某个项目的 `.claude/agents/`：

```bash
mkdir -p .claude/agents
cp prompts/multi-agent/subagent-*.md .claude/agents/
```

`main-agent.md` 不是子 agent 定义，建议作为主会话启动提示词使用。

## 推荐使用顺序

1. 把 `main-agent.md` 贴给主 agent。
2. 主 agent 完成上下文读取和领域模型定义。
3. 如果需要并行分析，把 `subagent-requirement-context-analyst.md` 交给子 agent。
4. 你确认领域模型和技术方案后，主 agent 开始实现。
5. 实现完成后，把 `subagent-test-reporter.md` 交给测试子 agent。
6. 如果测试失败，把测试报告交给 `subagent-repair-advisor.md`。
7. 主 agent 根据修复建议做最多 3 轮有限修复。
8. 最终有时间时使用 `subagent-final-reviewer.md` 复核。

## 重要边界

默认不要让子 agent 写代码。只有当任务边界非常清楚，并且你明确指定文件所有权时，才允许某个子 agent 修改文件。
