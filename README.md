# QA Agent Specification

> 如果未来团队里有一个 AI 测试工程师，我们应该如何把 QA 的经验教会它？

这是一套**开放规范**，用来把 QA 的隐性经验，工程化成 AI Agent 能够理解、执行、演进的 **Skill**。

它不是 prompt 合集。Prompt 会随模型过期；规范、设计模式、失败模式和评测体系不会。

## 为什么做这个

大多数团队接入 AI 做测试的方式，是攒一堆 prompt：换个模型就得重写，换个人就看不懂，出了错也说不清哪里错。

QA 的价值从来不在"点点点"，而在**发现风险、总结规律、定义质量标准**。这些经验大多是隐性的，藏在资深测试的判断里。AI 不会自动继承它——除非我们把它设计成可复用的 Skill。

这个仓库定义的，就是"怎么设计一个高质量的 QA Skill"。

## 仓库结构

```
qa-agent-spec/
├── SPECIFICATION.md        # 核心规范：一个 Skill 长什么样
├── spec/
│   ├── metadata.md         # 元数据：成熟度、版本、框架无关约定
│   ├── failure-patterns.md # ★ 失败模式：本项目的护城河
│   └── evaluation.md       # 评测体系：怎么判断一个 Skill 好不好
├── templates/
│   └── SKILL_TEMPLATE.md   # 统一模板，写新 Skill 从这里 copy
├── patterns/               # Agent 设计模式（单评审 / 计划-执行 / 评审循环 / …）
├── skills/                 # Skill 库（每个 Skill 一个目录）
└── examples/               # 完整案例
```

## 从哪读起

- 想理解设计哲学 → [`SPECIFICATION.md`](./SPECIFICATION.md)
- 想直接写一个 Skill → [`templates/SKILL_TEMPLATE.md`](./templates/SKILL_TEMPLATE.md)
- 想看什么是这个项目最不一样的地方 → [`spec/failure-patterns.md`](./spec/failure-patterns.md)

## 设计原则

1. **每个 Skill 都要说清"为什么"**，不止"怎么做"。
2. **框架无关**：不绑定任何模型或平台（OpenAI / Claude / Gemini / Cursor / …）。这条约束同时保证了规范里没有任何组织特定的实现细节。
3. **失败模式是一等公民**：记录最容易误判的地方和正确判断路径，而不只是理想流程。
4. **可评测、可演进**：每个 Skill 有成熟度和版本，能被打分，能迭代。
5. **反静默省略**：凡是逐项覆盖的动作都要留痕——查过没问题的显式标注、跳过的写明理由。沉默会被误读成"已覆盖"，那是漏测的根源。

## License

MIT
