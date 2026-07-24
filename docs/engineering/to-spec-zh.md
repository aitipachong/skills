快速开始：

```bash
npx skills add mattpocock/skills --skill=to-spec
```

```bash
npx skills update to-spec
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-spec)

## 它的作用

`to-spec` 把当前对话以及你对代码库的理解转化成一份 spec（你可能更熟悉 PRD 这个叫法），然后发布到你的 issue 追踪器中。

它**不会**再采访你一轮。等你用到它的时候，对齐工作已经完成了——`to-spec` 是把已经明确的东西综合成文，而不是重新问一轮问题。

## 什么时候用它

你通过输入 `/to-spec` 来调用它——agent 不会自己主动使用它。

当一个改动已经讨论清楚、领域语言已经统一，并且你想在写任何代码之前把这份共识写下来时，就该用它了。如果你们*还没*对齐，先去 grill——用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。要把写好的 spec 拆成 ticket，用 [to-tickets](https://aihero.dev/skills-to-tickets)。

## 前置条件

`to-spec` 会把内容发布到你的 issue 追踪器，所以必须先用 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 为这个仓库配置好追踪器和分诊标签。它会自己打上 `ready-for-agent` 标签——不需要再单独跑一遍分诊。

## spec 包含什么

- **问题陈述**——哪里坏了或缺了什么，以及为什么值得解决，用项目自己的词汇来写。
- **解决方案**——修复方案的高层形态，不涉及任何实现细节。
- **用户故事**——一份详尽的、带编号的清单，列出这个改动必须支持的具体行为，每一条都可以独立验证。
- **实现决策**——对话中已经敲定的选择，这样以后就不会再被翻出来重新争论。
- **测试决策**——这个特性将在哪些接缝（seam）处被测试，以及"完成"长什么样。
- **范围之外的事项**——这个改动*刻意不*覆盖什么，让 ticket 保持边界清晰。
- **补充说明**——任何其他值得带着走、但又不属于以上各节的内容。

## 深模块

在写 spec 之前，`to-spec` 会先勾勒这个特性将要被测试的**接缝**，并寻找**深模块**的机会——把大量功能藏在一个小而稳定的接口背后。它倾向于复用已有的接缝而不是新开一个，并且倾向于尽可能高的接缝，理想情况下整个改动只有一个。

这对 agentic 开发很重要：一个好的接口给了测试一个稳定的目标，这样接口之下的代码怎么变，测试都不用跟着动。

## 如何判断它工作正常

- 它直接开始写 spec，而不是重新问你一轮问题。
- 它在动笔前会和你确认接缝，并且提出的接缝尽可能少。
- 写出来的 spec 用的是你项目的领域词汇，而不是泛泛的模板腔。

## 它在流程中的位置

`to-spec` 是主构建链中的一步：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

在计划和领域语言都已确定之后、把工作拆成实现 ticket 之前用它。它的近邻是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)（打磨上下文，让 spec 更精确）和 [to-tickets](https://aihero.dev/skills-to-tickets)（把 spec 变成一组 ticket，交给 [implement](https://aihero.dev/skills-implement) 去构建）。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
