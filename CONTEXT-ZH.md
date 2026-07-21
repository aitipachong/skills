# Matt Pocock 技能集（Skills）

一组由 Claude Code 加载的智能体技能（斜杠命令与行为）。技能被组织进不同的桶（bucket），并由 `/setup-matt-pocock-skills` 生成的、针对每个仓库的配置来消费。

> 译者注：本文是一份**领域术语表**（共享语言）。加粗的英文术语是「规范术语」，翻译中保留英文原词以免破坏其作为术语的功能，括号内为中文释义。

## 语言（Language）

**Issue tracker**（issue 跟踪器）：
承载一个仓库 issue 的工具 —— GitHub Issues、Linear、一个本地 `.scratch/` 的 markdown 约定，或类似的东西。像 `to-tickets`、`to-spec`、`triage` 和 `qa` 这样的技能会对它进行读取和写入。
_避免使用_：backlog manager、backlog backend、issue host

**Issue**：
**Issue tracker** 内一个被追踪的工作单元 —— 一个 bug、一项任务、一份规格，或由 `to-tickets` 产出的一个切片。
_避免使用_：ticket（仅在引用那些把 issue 称为 ticket 的外部系统时使用，或用于 **Decision ticket** —— 见下文）

**Decision ticket**（决策工单）：
一个 `wayfinder` 单元 —— 是 `wayfinder:map` 的子 **Issue**，承载一个*问题*，其解决方案是一个「决策」，而不是要执行的一段构建切片。**decision（决策）**这个限定词，正是让它有别于「实现工单（implementation ticket）」的关键；`wayfinder` 会先引入这个术语，之后就简称 "ticket"。

**Triage role**（分拣角色）：
在分拣（triage）过程中应用到某个 **Issue** 上的规范化状态机标签（例如 `needs-triage`、`ready-for-afk`）。每个角色都通过 `docs/agents/triage-labels.md` 映射到 **Issue tracker** 中的一个真实标签字符串。

## 关系（Relationships）

- 一个 **Issue tracker** 承载多个 **Issue**
- 一个 **Issue** 同一时刻只携带一个 **Triage role**
- 一个 **Decision ticket** 是一个 **Issue**（是某个 `wayfinder:map` 的子项）

## 已标记的歧义（Flagged ambiguities）

- "backlog" 此前既被用来指代承载 issue 的*工具*，又被用来指代其中的*工作整体* —— 已解决：工具称为 **Issue tracker**；"backlog" 不再作为领域术语使用。
- "backlog backend" / "backlog manager" —— 已解决：已合并进 **Issue tracker**。
