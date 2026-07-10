---
name: <skill-name>
version: 0.1
maturity: prototype   # prototype | stable | production | recommended | best-practice
frameworks: [any]     # 目标框架，保持无关时写 any
depends_on: []        # 前置 Skill / 能力，没有就留空
---

# <Skill 名称>

## Why — 为什么需要
<这个 Skill 解决什么问题？不用它，测试会漏掉什么、错判什么？>

## When — 何时使用
**用它当：**
- <触发场景 1>
- <触发场景 2>

**不要用它当：**
- <边界外场景，交给哪个 Skill / 谁>

## Input — 输入契约
- <需要的输入，及格式>
- **前置条件：** <执行前必须成立的状态>

## Process — 执行流程
1. <步骤>
2. <步骤——在关键判断点标注：这里为什么这么判断>
3. <步骤>

> 关键判断点：<列出流程里最容易走错、需要经验的分叉，及正确走法>

## Output — 完成定义
- **交付物：** <产出长什么样>
- **完成标准：** <怎样算这个 Skill 执行成功>

## Failure Patterns — 失败模式
| 现象 | 容易的误判 | 正确判断路径 |
|---|---|---|
| <观察到什么> | <会被错当成什么> | <应该怎么判断> |

## Examples
见 `examples/`。
