# Contributing

欢迎贡献 Skill、设计模式、失败模式和评测改进。

## 加一个新 Skill

1. 从 [`templates/SKILL_TEMPLATE.md`](./templates/SKILL_TEMPLATE.md) 复制，建 `skills/<name>/SKILL.md`。
2. 五问（Why / When / Input / Process / Output）写全，别省。
3. **至少写一条真实的 Failure Pattern**——现象 / 误判 / 正确路径三列。这是硬性要求，不是加分项。
4. 在 `examples/` 放一个真实输入 → 期望输出的样例。
5. 对着 [`spec/evaluation.md`](./spec/evaluation.md) 自评，把分数和成熟度写进 PR。

## 一条底线：框架无关 + 不含组织特定信息

Skill 描述测试意图和判断逻辑，**不写**任何具体工具名、内部账号、私有基础设施、平台专属 API。

自检一句：**"换一个团队、换一套工具链，这条还成立吗？"** 不成立的属于私有适配层，不进这个仓库。

## 提 PR

- 一个 PR 聚焦一件事（一个 Skill / 一个模式 / 一批失败模式）。
- 说清你改了什么、为什么。
