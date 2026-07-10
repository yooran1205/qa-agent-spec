# Agent Design Patterns — Agent 设计模式

Skill 是单个能力。当一件测试工作需要多步、多角色协作时，怎么把 Agent 组织起来，是另一层设计问题。

这里沉淀常见的协作模式——不是具体实现，而是"什么场景该用什么结构"。

| 模式 | 一句话 | 适合 |
|---|---|---|
| **Single Review Agent** | 一个 Agent 独立完成一次评审 | 简单、边界清晰的检查（如单份 PRD 评审） |
| **Planner–Executor** | 一个负责拆解计划，一个负责执行 | 任务需要先规划再落地（如生成回归计划 → 执行） |
| **Review Loop** | 产出 → 评审 → 修正，循环到收敛 | 质量要求高、一次做不对的产物 |
| **Critic Pattern** | 独立的"挑刺者"专门反驳主 Agent 的结论 | 防止自信的错误结论（尤其 bug 判定） |
| **Multi-Agent Testing** | 多个 Agent 分工覆盖不同测试维度，再汇总 | 大范围回归、需要并行覆盖 |

每个模式建议单独成文，说明：**解决什么协作问题、什么时候用、什么时候会过度设计。**

> 为什么 Critic Pattern 值得单列：测试里最贵的错误是"假阳性通过"和"误判根因"。让一个独立角色专门反驳，比让同一个 Agent 自查更能拦住这类错误——这正好呼应 [`../spec/failure-patterns.md`](../spec/failure-patterns.md)。
