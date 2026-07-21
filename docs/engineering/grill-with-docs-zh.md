快速开始：

```bash
npx skills add mattpocock/skills --skill=grill-with-docs
```

```bash
npx skills update grill-with-docs
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs)

## 它做什么

`grill-with-docs` 会围绕一个计划或设计对你进行穷追不舍的访谈，一次只问一个问题，直到你和智能体达成共识——并且它会边问边把术语和决策记录下来。

这场拷问会**留下纸面轨迹**。普通的访谈能磨砺你的思考，但会话一结束就烟消云散；而这个技能会在每个术语被敲定的那一刻就把它写入 `CONTEXT.md` 术语表，并把那些艰难的、不可逆的决策记录为 ADR（架构决策记录）。共识因此得以在对话之外存活，而不是只活在你的脑子里。

## 什么时候用它

通过输入 `/grill-with-docs` 来调用——智能体不会主动使用它。

在改动刚刚开始、计划还很模糊、领域语言尚未定型的时候用它，趁任何代码还不存在，把计划和术语都压力测试一遍。如果你只想要访谈、不需要产物，用 [grilling](https://aihero.dev/skills-grilling)；如果计划已经清晰、只需要敲定或记录术语，用 [domain-modeling](https://aihero.dev/skills-domain-modeling)。而如果改动大到单个会话装不下、路线依然迷雾重重——比如全新项目、巨型功能开发——请先从上游的 [wayfinder](https://aihero.dev/skills-wayfinder) 开始：它会把整个工程绘制成一张决策地图，等路线清晰后再交回主流程。

## 前置条件

这个技能是有状态的——它会边拷问边写入你的仓库。敲定下来的术语会进入根目录的 `CONTEXT.md` 术语表（如果 `CONTEXT-MAP.md` 标记了多上下文仓库，则写入对应上下文的 `CONTEXT.md`），而真正难以逆转的决策会以 ADR 的形式落在 `docs/adr/` 下。两者都是惰性创建的——在第一个术语或决策成型之前什么都不存在——所以你不需要提前搭任何脚手架，但你需要身处一个可以安全写入这些文件的地方。

## 拷问机制

引擎是一场**拷问（grill）**：沿着决策树一次只问一个问题、穷追不舍，在往下走之前先解决决策之间的依赖关系，并且每个问题都会附带一个推荐答案。凡是代码库能回答的问题，它会去读代码库来回答，而不是来问你。

让这个变体成为独立技能的关键，在于答案的去向。随着拷问进行，模糊的语言被磨砺成规范术语，并即时写入术语表——而不是攒到最后批量处理。术语表始终保持为纯粹的术语表：只有词汇，没有实现细节，没有规格说明。ADR 的提议非常克制，只在一个决策难以逆转、缺少上下文会令人意外、且确实是真实权衡的结果时才会提出。大多数会话产出的只是一个更锋利的术语表，以及很少甚至没有 ADR——这正是预期的形态。

## 生效的标志

- 它一次只问一个问题并耐心等待，而不是甩出一张问卷。
- 术语在敲定的瞬间就被写入 `CONTEXT.md`，用的是你项目自己的语言。
- 它会主动深入代码库，自己回答能回答的问题。
- ADR 保持稀有——你不会被要求给可逆的选择盖章背书。

## 它处于什么位置

`grill-with-docs` 是主构建链的第一步：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它排在最前，先于任何被写成规格的东西：它产出的共识和定型的术语，让 [to-spec](https://aihero.dev/skills-to-spec) 可以直接综合成规格，而不必重新访谈你。它的近邻是 [grilling](https://aihero.dev/skills-grilling)——同样这套访谈、但没有文档产物——以及 [domain-modeling](https://aihero.dev/skills-domain-modeling)——它所驱动的那套术语表与 ADR 纪律。当你不确定哪个技能或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
