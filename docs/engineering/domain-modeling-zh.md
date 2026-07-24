快速开始：

```bash
npx skills add mattpocock/skills --skill=domain-modeling
```

```bash
npx skills update domain-modeling
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling)

## 它的作用

`domain-modeling` 在你做设计的过程中，构建并打磨项目的**统一语言**（ubiquitous language）——挑战含糊的术语，用具体场景对概念间的关系做压力测试，并在语言刚刚成形的那一刻把词汇表和决策写下来。

这是**主动**的纪律，而不是被动的。仅仅读一读 `CONTEXT.md` 借用其中的词汇，是任何 skill 一行就能做到的习惯；这个 skill 面向的是当你正在*改变*模型的时候——要敲定一个规范术语、发现代码和你刚说出口的话之间存在矛盾、要记录一个难以逆转的决策。同时它也保持词汇表的干净：`CONTEXT.md` 只是词汇表，别无他物——没有实现细节，没有规格说明，也不是草稿本。

## 什么时候用它

输入 `/domain-modeling` 调用它，或者当任务契合时 agent 会自动选用它——当你正在敲定术语、消解一个被过度负载的词，或记录一项架构决策时。

当*措辞*本身就是问题时用它：两个人说的 "cancellation" 不是一回事，"account" 同时扛着三份工作，或者一场设计讨论总是在一个从未被精确定义的概念上卡住。如果问题出在模块的*形态*上——接缝划在哪里、接口该有多深——那就用 [codebase-design](https://aihero.dev/skills-codebase-design)。如果你希望在动手构建之前先对计划本身做一番拷问，用 [grilling](https://aihero.dev/skills-grilling)。

## 前置条件

这个 skill 会写入两个位置，都是惰性创建的——只有真正有东西要记录时才会创建。敲定的术语进入仓库根目录的 `CONTEXT.md`（或者，在由 `CONTEXT-MAP.md` 标记的多上下文仓库中，进入各上下文自己的 `CONTEXT.md`）。决策进入 `docs/adr/`。事先什么都不需要存在；第一个敲定的术语会创建词汇表，第一个真正的权衡会创建 ADR。

## 词汇表 vs. ADR

两种产物，两套不同的门槛：

- **词汇表**（`CONTEXT.md`）承载语言。每当一个含糊的词被敲定为规范术语，就立刻就地写入——不攒批——让共享词汇始终与对话保持同步。它毫不留情地剔除实现细节。
- **ADR** 承载决策，而且门槛很高：只有当这个选择**难以逆转**、**缺少上下文时令人意外**、并且**是真实权衡的结果**时才会提出。三条少任何一条，就没有 ADR。正是这一点让 `docs/adr/` 成为重大岔路口的记录，而不是一本日记。

让它真正奏效的招式是：当你陈述某样东西如何运作时，这个 skill 会交叉对照代码，把矛盾摆到台面上——"你的代码取消的是整个订单，但你刚才说部分取消是可能的——到底哪个对？"语言与代码被强制达成一致。

## 有意拆出来的原因

`domain-modeling` 是构建项目统一语言的**唯一权威来源**，被刻意拆成一个独立的、可被模型调用的 skill，好让任何其他 skill 都能触达它。[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 依赖它在 grilling 会话进行中记录术语和决策，[triage](https://aihero.dev/skills-triage) 用它让工单保持用项目自己的语言书写，[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在工作过程中也会用到它。

保持独立也意味着你可以直接取用——把它当作一份关于如何打磨模型的**参考**——而不必承诺执行那些 skill 所规定的步骤。语言只存放在一个地方，需要它的一切都指向那里。

## 它在流程中的位置

`domain-modeling` 是一个**随时可取用的独立 skill**，它运行在别的 skill *之下*的频率，和作为固定步骤运行的频率一样高。它最亲近的邻居是 [codebase-design](https://aihero.dev/skills-codebase-design)，因为共享的语言正是让你能精确命名一个深模块及其接缝的东西；在下游，一份沉淀好的词汇表恰好是 [to-spec](https://aihero.dev/skills-to-spec) 用来合成一份用项目自己的语言写成的规格的原料。当你不确定哪个 skill 或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
