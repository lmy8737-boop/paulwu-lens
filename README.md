# paulwu-lens：用吴鼎文（PaulWu）的公开方法论解读价值、红利、左侧标的

> **非官方 · 实验性 · 复现验证未通过 · 不构成投资建议**
> 一份给 AI agent 用的 skill：把一只偏价值、红利、左侧的股票，放进吴鼎文（沁源投资 / Headwater）公开发表的原则里做解读，输出研究假设、证据缺口和待核实问题。它不会告诉你买还是卖，也不会替他表态。
>
> *English, briefly: an unofficial agent skill that reads value / dividend / left-side stocks through the publicly written principles of PaulWu (Wu Dingwen). It outputs research hypotheses, evidence gaps and questions to verify — never buy/sell calls. Its reproduction test did not pass; treat it as an experimental questioning aid, not a validated tool.*

## 它做什么

给定一只你选的标的（和你已经查到的数据），按他公开文字里的方法逐栏追问：

| 栏 | 问什么 | 来自 |
|---|---|---|
| A | 回收期与机会成本：现在的机会成本是多少，多久收回投资 | M03、M04 |
| B | 现金流真实性与股东回报：分红来自经营现金流，还是卖资产、借钱；回购规模；管理层兑现 | M05 |
| C | 高息与低估陷阱：行业格局、行政垄断、泡沫底层加杠杆、周期高点现金流、烟蒂三问 | M06 |
| D | 效率差与存续：便宜是否值得 | M02 |
| E | 左侧前提与逻辑退出：能否复盘涨跌；仓位上限、分散、流动性；退出看逻辑不看价格 | M08、M09、M11 |
| F | 对立面与自检：最强反方；是不是在为已有仓位找理由 | M07、M12 |

然后给 2–3 句总体研究假设、最像的失败档案、与你自有规则的冲突提示，以及至多 5 条待裁决的研究假设。每条判断都标 `[Mxx]`（来自他的公开原则）或 `[推断]`（我的推断），没有标注的判断不允许出现。

## 它不做什么

- 不给买入、卖出、加仓、减仓、仓位、目标价。
- 不说"他会买/他会卖"。
- 不用于景气度追热点、短线交易、选股筛选、量化回测。
- 不使用二手转述里一手找不到的框架（三表读法、假账公式、A·B·C 仓位矩阵、四档资本配置、成列的六条做空规则）。

## 状态：请先读这一节

- **复现验证未通过。** 预先登记标准后做了留出集盲评：v0.1 命中 11/27，同模型无 skill 的基线 14/27；v0.2 修订后探索性重跑 18/27（基线 15/27），差距 +11.1 个百分点，仍低于预登记的 +15 个百分点，并且修订依据就是留出集的失分，含过拟合成分。详见 [VALIDATION.md](VALIDATION.md)。
- **方法有效性未验证。** 他的案例是自己的事后叙述，存在幸存者偏差；这个仓库测的最多是"能不能复现他的推理"，不是"这套方法赚不赚钱"。
- **A 股适用性未校准。** 他的方法建在能做空、能对冲的海外基金上，自述市场有效性美 ≫ 港 > 中。
- 范围已按使用场景收窄为价值、红利、左侧；收窄之后没有重新盲评。

所以更合适的用法是：**把它当作一份追问清单的生成器**，帮你想到没想到的问题；不要把它的结论当作"他的看法"或"验证过的方法"。

## 安装

Claude Code：

```bash
git clone https://github.com/lmy8737-boop/paulwu-lens ~/.claude/skills/paulwu-lens
```

其他支持 skill 目录的 agent：把仓库放进它的 skills 目录即可，入口是 `SKILL.md`。没有 skill 机制的对话模型：把 `SKILL.md` 和 `references/` 下的文件贴进对话开头。

使用时直接说：

> 用 PaulWu 视角解读一下 XX（说明你已有的数据：估值、股息、现金流、持仓成本等）

数据要你自己提供或让 agent 用你环境里的行情和财务工具取；skill 本身不取数，也不会编造输入里没有的数字。

## 目录

```
SKILL.md              入口：红线 D1–D7、流程、输出模板
references/
  checklist.md        12 条方法论主张（M01–M12）与逐条追问的检验问题
  anchors.md          他在不同年份用过的息率、市盈率参照（转述，带日期，不是阈值）
  examples.md         6 个示范案例（转述）
  cases.md            训练集案例一句话（18 例）
  conflicts.md        他的主张与常见的对立做法（K1–K6），交给使用者裁决
  sources.md          来源编号 S01–S43 对应的文章标题、日期和雪球链接
VALIDATION.md         预登记的验证协议与结果（含失败）
DISCLAIMER.md         声明
CHANGELOG.md          版本记录
```

## 来源与版权

所有来源都是他在雪球公开发表的专栏、官方 Q&A 和一份访谈提纲，加上 SEC 披露的 13F；二手转述中一手找不到的内容已隔离，不使用。仓库**不含原文**，只含转述、归纳和书目信息（`references/sources.md`）。原文版权归吴鼎文，请到雪球阅读。如有不当请提 Issue，会立即处理。详见 [DISCLAIMER.md](DISCLAIMER.md)。

## 许可

仓库中作者原创的文字（检验清单措辞、转述、模板）按 MIT 许可发布，见 `LICENSE.txt`。该许可不涵盖吴鼎文的任何原文。
