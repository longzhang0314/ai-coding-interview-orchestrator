# Quick Prompts

Use these prompts when you want explicit control in Claude Code. In normal interviews, the short invocation is enough:

```text
使用 ai-coding-interview-orchestrator。
```

Then paste the screenshot, README, requirement text, or code.

## Full Start Prompt

```text
使用 ai-coding-interview-orchestrator。

我正在进行 AI Coding 面试/笔试。下面是题目截图、README 或现有代码。
请严格按以下流程执行：
1. 读取题目和代码结构
2. 复述需求和验收目标
3. 抽象业务模型
4. 写极简 spec
5. 写文件级实现计划
6. 暂停并让我人工审查任务拆解和修改范围
7. 我确认后再实现核心闭环
8. 运行最小验证
9. 输出交付说明

需求不清晰时最多问 1 个关键问题；如果我没有回答，请基于合理假设继续。
验证失败后最多做 2 轮修复和重新验证；仍失败就停止并输出受控未完成报告。
优先可运行、可解释、可验收，不要过度设计。
```

Use the full version only when the current session seems not to follow the skill contract.

## Continue After Requirements Are Understood

```text
继续使用 ai-coding-interview-orchestrator。
我已确认刚才的 spec 和文件级计划。请开始实现核心闭环，完成后运行最小验证命令。
```

## Skip Review For This Run

```text
继续使用 ai-coding-interview-orchestrator。
本次跳过人工审查门，按你刚才的计划直接实现并验证。
```

## Expand Repair Budget

```text
继续使用 ai-coding-interview-orchestrator。
本次允许最多 4 轮修复验证；每轮修复后只跑最小相关验证命令。
```

## Debug A Failed Run

```text
继续使用 ai-coding-interview-orchestrator，并按系统化调试方式处理这个失败。
先复述错误，再提出一个最可能假设，只做一个针对性修改，然后重跑最小验证命令。
```

## Finalize For Interviewer

```text
使用 ai-coding-interview-orchestrator 做最终交付检查。
请输出：完成内容、修改文件、运行方式、验证结果、关键假设、风险和后续扩展。
语气要像我在向面试官汇报，不要写太长。
```
