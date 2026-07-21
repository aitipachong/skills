快速开始：

```bash
npx skills add mattpocock/skills --skill=grilling
```

```bash
npx skills update grilling
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling)

## 它是做什么的

`grilling` 是一场毫不留情的访谈，在你动手构建之前，对计划或设计进行压力测试。它沿着决策树一个分支一个分支地走，逐个解决决策之间的依赖关系，直到你和智能体达成共识。

它**一次只问一个问题**，等你回答后才问下一个——绝不会一次性抛出一堆问题，那样会让人不知所措。每个问题都会附带智能体自己的推荐答案，任何代码库能解决的问题它都会自己去探索，而不是来问你。在你确认双方已达成共识之前，它不会开始执行计划。

## 什么时候用它

输入 `/grilling`，或者当任务合适时智能体会自动调用它——这是底层的原语（primitive），不是仅供用户使用的入口。

当计划或设计还存在薄弱环节，而你希望在写代码之前把它们暴露出来时，就用它。实际上，你通常是通过它的两个封装器之一来使用它，而不是直接叫它的名字：想要一场纯粹的拷问式访谈，用 [grill-me](https://aihero.dev/skills-grill-me)；想让访谈过程中同时编写 ADR（架构决策记录）和术语表，用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。

## 决策树

其心智模型是一棵**决策树**：每个计划都会分支出若干决策，而决策之间相互依赖。`grilling` 一次下降一个节点，因此早期的回答可以重塑接下来的问题。这就是为什么问题逐个到来、并按依赖顺序排列——一股脑地并行提问会丢失让访谈收敛到共识的结构。

## 为什么要单独拆分出来

`grilling` 是访谈技巧的**唯一事实来源**，被拆分为一个由模型调用的**原语**，这样每个需要访谈的 skill 都可以直接调用它，而不是重新造轮子。[grill-me](https://aihero.dev/skills-grill-me) 和 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 是它的两个用户入口，而 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 和 [triage](https://aihero.dev/skills-triage) 也借助它来对自己的决策进行压力测试。

把访谈技巧集中在一个地方，也意味着当你只想要访谈本身时，可以直接调用它——不需要它的封装器额外附加的 ADR 编写或工单整理功能。

## 它在整个流程中的位置

`grilling` 是主要构建链之下的访谈**原语**：[grill-with-docs](https://aihero.dev/skills-grill-with-docs) 在 [to-spec](https://aihero.dev/skills-to-spec) 撰写规范之前运行它，以理清上下文。当你不确定该用哪个入口时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
