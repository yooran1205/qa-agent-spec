# Metadata — 元数据

每个 Skill 顶部用 YAML frontmatter 声明元数据，让使用者一眼看清它的成熟度、版本和依赖。

```yaml
---
name: generate-test-case
version: 1.0
maturity: production
frameworks: [any]
depends_on: [review-prd]
---
```

## 成熟度（maturity）

告诉使用者这个 Skill 可信到什么程度。

| 等级 | 含义 |
|---|---|
| ⭐☆☆☆☆ `prototype` | 原型，能跑通一次，未经反复验证 |
| ⭐⭐☆☆☆ `stable` | 稳定，多场景验证过，边界仍有盲区 |
| ⭐⭐⭐☆☆ `production` | 可用于真实工作流 |
| ⭐⭐⭐⭐☆ `recommended` | 推荐做法，经过评测且有失败模式沉淀 |
| ⭐⭐⭐⭐⭐ `best-practice` | 最佳实践，作为同类 Skill 的参照标准 |

成熟度不是自封的——它应该由 [`evaluation.md`](./evaluation.md) 的评分支撑。

## 版本（version）

Skill 会演进。用版本记录它怎么变好的。

```
generate-test-case
  v0.1  仅覆盖正向用例
  v0.2  加入边界值与异常路径
  v1.0  加入失败模式表，通过评测
```

破坏性变更（输入契约变了、输出格式变了）升主版本；能力增强升次版本。

## 依赖（depends_on）

声明这个 Skill 依赖哪些前置 Skill 或能力。让 Agent 能编排、让使用者知道要先准备什么。

## 框架（frameworks）

保持框架无关时写 `[any]`。只有当某个 Skill 确实针对特定生态时才具体标注——但那通常意味着它该被拆成"通用规范 + 私有适配层"两部分。
