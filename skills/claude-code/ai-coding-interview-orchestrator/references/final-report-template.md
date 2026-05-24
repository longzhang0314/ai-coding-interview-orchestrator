# Final Report Template

Use this shape at the end of an AI coding interview task.

```markdown
完成了。核心闭环是：<一句话说明结果>。

修改内容：
- <文件/模块>：<做了什么>
- <文件/模块>：<做了什么>

运行方式：
```bash
<command>
```

验证方式：
```bash
<command>
```

验证结果：
- <通过/未能运行及原因>

修复轮次：
- <0/1/2 轮；如果达到上限，说明停止原因>

关键假设：
- <需求不明确处的处理方式>

风险和后续扩展：
- <当前限制>
- <如果继续做，下一步是什么>
```

## Controlled Incomplete Report

If verification still fails after the repair budget, do not keep fixing automatically. Use this form:

```markdown
当前已停止自动修复，原因是验证失败已达到默认 2 轮修复上限。

已完成：
- <已经实现并保留的功能>

已通过验证：
- <通过的检查或样例>

仍失败：
- <失败命令或失败点>

已尝试修复：
- 第 1 轮：<改了什么，结果如何>
- 第 2 轮：<改了什么，结果如何>

判断：
- <核心功能是否可用>
- <最可能的剩余原因>

建议下一步：
- <需要用户/面试现场决定的最小动作>
```

## Interview Delivery Notes

- Be honest about unverified parts.
- Mention why the design is intentionally small.
- If the task includes optional AI behavior, explain the mock/provider boundary.
- If tests cannot run due to environment or dependency limits, state exactly what was checked instead.
