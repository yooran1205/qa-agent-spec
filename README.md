# QA Agent Specification

> 如果未来团队里有一个 AI 测试工程师，我们应该如何把 QA 的经验教会它？

这是一套**开放规范**，用来把 QA 的隐性经验，工程化成 AI Agent 能够理解、执行、演进的 **Skill**。

它不是 prompt 合集。Prompt 会随模型过期；规范、设计模式、失败模式和评测体系不会。

## 为什么做这个

大多数团队接入 AI 做测试的方式，是攒一堆 prompt：换个模型就得重写，换个人就看不懂，出了错也说不清哪里错。

QA 的价值从来不在"点点点"，而在**发现风险、总结规律、定义质量标准**。这些经验大多是隐性的，藏在资深测试的判断里。AI 不会自动继承它——除非我们把它设计成可复用的 Skill。

这个仓库定义的，就是"怎么设计一个高质量的 QA Skill"。

## 三层结构：规范 · 技能 · 模式

这个项目不是一堆并列的条目，而是一套**有内核、能贯穿**的方法论，分三层：

| 层 | 是什么 | 回答 |
|---|---|---|
| **规范（Spec）** | 一个高质量 Skill / 模式长什么样、怎么评分 | "什么是好" |
| **技能（Skill）** | 遵循规范的可复用测试能力 | "具体怎么做一件事" |
| **模式（Pattern）** | 多个 Agent 如何协作 | "多步 / 多角色时怎么组织" |

三层不是各写各的——同一个方法论内核会**竖直贯穿**它们。以本项目的核心观点"**测试里最贵的错误是自信的误判**"为例，它在三层里各有落点：

```
规范   spec/failure-patterns.md   —— 把"最容易误判的地方 + 正确判断路径"定为一等公民
  │
技能   skills/analyze-bug         —— 用"根因假设 + 证伪测试"把不确定性显式化，不假装唯一答案
  │
模式   patterns/critic-pattern    —— 把证伪放大成独立 Agent，专职反驳、拦住自信的错误结论
```

**能看到一个观点从规范贯穿到技能再到模式**——这就是它区别于"prompt 合集 / 资料整理"的地方。

## 仓库结构

```
qa-agent-spec/
├── SPECIFICATION.md            # 核心规范：一个 Skill 长什么样（含"反静默省略"等通用约定）
├── spec/
│   ├── failure-patterns.md     # ★ 失败模式：本项目的护城河
│   ├── evaluation.md           # 评测体系：可复现拆成"过程 / 结论"两层
│   └── metadata.md             # 元数据：成熟度、版本、框架无关约定
├── templates/
│   └── SKILL_TEMPLATE.md       # 统一模板，写新 Skill 从这里 copy
├── patterns/                   # Agent 设计模式
│   └── critic-pattern.md       # 已成文样板（其余 4 个待补）
└── skills/                     # Skill 库（三种形状，均 best-practice）
    ├── generate-test-case/     # 生成型
    ├── analyze-bug/            # 诊断型
    └── review-prd/             # 评估型
```

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
- 想看方法论如何贯穿三层 → 上面「三层结构」里那个竖直示例，再顺着读 `analyze-bug` 与 `critic-pattern`

## 设计原则

1. **每个 Skill 都要说清"为什么"**，不止"怎么做"。
2. **框架无关**：不绑定任何模型或平台（OpenAI / Claude / Gemini / Cursor / …）。这条约束同时保证了规范里没有任何组织特定的实现细节。
3. **失败模式是一等公民**：记录最容易误判的地方和正确判断路径，而不只是理想流程。
4. **可评测、可演进**：每个 Skill 有成熟度和版本，能被打分，能迭代。
5. **反静默省略**：凡是逐项覆盖的动作都要留痕——查过没问题的显式标注、跳过的写明理由。沉默会被误读成"已覆盖"，那是漏测的根源。

## License

MIT
