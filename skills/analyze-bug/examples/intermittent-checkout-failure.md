# Example: 偶发下单失败

一个刻意通用、不含任何具体项目信息的样例，展示 `analyze-bug` 怎么把回声和根因分开。

## 输入（缺陷报告）
> 用户偶尔下单失败，页面弹"系统繁忙"。约每 20 单出现 1 次，无固定步骤。附一段服务日志：
> ```
> 12:03:01.120  ERROR  OrderService  NullPointerException at buildReceipt()
> 12:03:01.118  ERROR  OrderService  order total is null
> 12:03:01.090  WARN   PriceClient   fallback to cached price (upstream timeout)
> 12:03:00.030  WARN   PriceClient   call price-service timeout after 1000ms
> ```
> 报告人猜测：`buildReceipt()` 有空指针 bug。

## 输出（按输出契约）

| 字段 | 内容 |
|---|---|
| 现象 | 观察：偶发下单失败、弹"系统繁忙"。期望：下单成功或给出可重试的明确错误。（剥离报告人"buildReceipt 空指针"的猜测） |
| 复现类别 | **偶发**，置信度高（~5% 频率、无固定步骤 → 疑时序/依赖不稳，不是确定复现） |
| 证据链 | 按时间回溯：最醒目的是 12:03:01.120 的 NPE，但**最早异常点**是 12:03:00.030 的 `price-service timeout`。时间线：上游超时 → 12:03:01.090 回退到缓存价 → 缓存未命中致 `order total is null` → 传入 `buildReceipt()` 触发 NPE。NPE 是链末回声，不是起因。 |
| 根因假设 | **断言**：price-service 超时后的缓存回退在缓存未命中时返回 null 价格，未被校验即向下传递，最终在 buildReceipt 崩溃。置信度 **中**（时间线支持，但需确认缓存未命中路径）。 |
| 证伪测试 | 构造 price-service 超时 + 缓存未命中，若 total 非 null 或在回退处被拦截报错、不触发 NPE，则假设被推翻。 |
| 严重度 | 影响面：所有触发上游超时且缓存未命中的下单；频率：~5%。→ **中高**（影响交易主流程，但非全量）。 |
| 修复方向 | 针对根因：回退路径对 null 价格做校验并给明确可重试错误；而非仅在 `buildReceipt()` 加空判断（那只是盖住 NPE，用户仍下单失败）。 |

## 这个样例演示了什么
- **最早 ≠ 最醒目**：NPE 最扎眼，真起因是更早的上游超时。
- **剥离报告人猜测**："buildReceipt 空指针"是回声，照它修只会 masking。
- **修复方向对准根因**：在 `buildReceipt()` 加空判断能让 NPE 消失，但下单照样失败——这正是失败模式表里"改一下报错就没了"的陷阱。
- **不确定性显式化**：根因置信度标"中"并给了证伪测试，而不是假装唯一答案。
