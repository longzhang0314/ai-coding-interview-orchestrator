# Quick Prompts

Use these prompts when you want explicit control. In normal interviews, the short invocation is enough:

```text
请使用 $ai-coding-interview-orchestrator。
```

Then paste the screenshot, README, requirement text, or code.

## Full Start Prompt

```text
请使用 $ai-coding-interview-orchestrator。

我正在进行 AI Coding 面试/笔试。下面是题目截图、README 或现有代码。
请严格按以下流程执行：
1. 读取题目和代码结构
2. 复述需求和验收目标
3. 抽象业务模型
4. 写极简 spec
5. 写文件级实现计划
6. 实现核心闭环
7. 运行最小验证
8. 输出交付说明

需求不清晰时最多问 1 个关键问题；如果我没有回答，请基于合理假设继续。
优先可运行、可解释、可验收，不要过度设计。
```

Use the full version only when the current session seems not to follow the skill contract.

## Continue After Requirements Are Understood

```text
请继续使用 $ai-coding-interview-orchestrator。
基于刚才的 spec，按文件级计划开始实现。先做核心闭环，完成后运行最小验证命令。
```

## Debug A Failed Run

```text
请继续使用 $ai-coding-interview-orchestrator，并按 systematic debugging 的方式处理这个失败。
先复述错误，再提出一个最可能假设，只做一个针对性修改，然后重跑最小验证命令。
```

## Finalize For Interviewer

```text
请使用 $ai-coding-interview-orchestrator 做最终交付检查。
请输出：完成内容、修改文件、运行方式、验证结果、关键假设、风险和后续扩展。
语气要像我在向面试官汇报，不要写太长。
```
