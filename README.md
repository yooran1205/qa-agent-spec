# QA Agent Specification

> 如果团队里有个 AI 测试工程师，怎么把 QA 的经验教给它？

一套框架无关的开放规范，把 QA 经验工程化成可复用、可评测、可演进的 **Skill**——不是 prompt 合集。

## 结构

```
qa-agent-spec/
├── SPECIFICATION.md        # 一个 Skill 长什么样
├── spec/
│   ├── failure-patterns.md # 失败模式（护城河）
│   ├── evaluation.md       # 评测体系
│   └── metadata.md         # 成熟度 / 版本 / 框架无关
├── templates/SKILL_TEMPLATE.md
├── patterns/               # Agent 设计模式
└── skills/                 # Skill 库
```

三层（规范 / 技能 / 模式）贯穿同一内核。以「最贵的错误是自信的误判」为例：
`failure-patterns` → `analyze-bug`（证伪测试）→ `critic-pattern`（独立反驳）。

## Skills

| Skill | 形状 | 成熟度 |
|---|---|---|
| [generate-test-case](./skills/generate-test-case/) | 生成 | best-practice |
| [analyze-bug](./skills/analyze-bug/) | 诊断 | best-practice |
| [review-prd](./skills/review-prd/) | 评估 | best-practice |

## 规范要点

- **五问**：Why / When / Input / Process / Output
- **失败模式是一等公民**：现象 / 误判 / 正确路径
- **可复现分两层**：过程可复现（硬要求）/ 结论可复现（按类型）
- **反静默省略**：覆盖动作要留痕，跳过要写明理由
- **框架无关**：不绑定任何模型或平台

## 快速开始

- 写 Skill → copy [`templates/SKILL_TEMPLATE.md`](./templates/SKILL_TEMPLATE.md)
- 评分 → 对照 [`spec/evaluation.md`](./spec/evaluation.md)

## License

MIT
