快速开始：

```bash
npx skills add mattpocock/skills --skill=improve-codebase-architecture
```

```bash
npx skills update improve-codebase-architecture
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture)

## 它的作用

`improve-codebase-architecture` 会扫描代码库，寻找**加深机会（deepening opportunities）**——即那些浅模块（一个接口几乎和它要隐藏的东西一样复杂的模块）可以变成深模块的地方——然后把它们呈现为一份自包含的可视化 HTML 报告，再针对你选中的那一个展开追问（grill）。

它**不会**丢给你一份平平无奇的重构清单。每个候选都必须通过**删除测试（deletion test）**——删掉这个模块，是把复杂度*收敛*到更小的接口后面，还是只是把复杂度挪了个地方？只有"收敛"的情况才配拥有一张卡片。正是这个过滤器，让报告不会沦为泛泛而谈的清理建议。

除非你指定了特定区域，它还会自动聚焦到开发实际发生的地方——通过阅读最近的提交，偏向那些你仍在改动的代码。加深模块的回报在于让未来的改动更轻松，所以它会给仓库中近期有变动的部分赋予更高的权重。

## 什么时候用它

你可以通过输入 `/improve-codebase-architecture` 来调用它——agent 不会自己主动使用它。

把它当作一次周期性体检：每隔几天用一次，或者当一个代码库开始让人感觉"想理解一个概念得在好几个小模块之间跳来跳去"的时候。它读取现有架构，并提出在哪里加深它的建议。如果你已经知道想重新设计哪个模块，只是需要一套词汇来把它想清楚，请改用 [codebase-design](https://aihero.dev/skills-codebase-design)——这个 skill 是负责找出候选的调查员，那一个才是设计工作台。

## 加深机会

整个 skill 都围绕一个概念展开：**深度（depth）**。深模块把大量功能藏在一个小而稳定的接口后面；浅模块则把实现泄漏到一个几乎和底下代码一样宽的接口里。报告猎捕的就是"浅"——只是为了可测试性而提取出来的纯函数，而真正的 bug 却藏在它们的调用方式里（没有**局部性 locality**）；跨越自身**接缝（seam）**泄漏的模块；不打开五个文件就无法理解的概念——并提出能够修复它的加深方案。

它使用共享的设计词汇（**模块 module**、**接口 interface**、**深度 depth**、**接缝 seam**、**适配器 adapter**、**杠杆 leverage**、**局部性 locality**），以及 `CONTEXT.md` 中你自己项目的领域语言，所以一个候选项读起来是"加深订单接入模块"，而不是"重构 FooBarHandler"。

## 先报告，再追问

输出是一个写入操作系统临时目录、可直接在浏览器中打开的 HTML 文件——不会有任何东西落进仓库。每个候选都是一张卡片，包含涉及的文件、摩擦点、通俗易懂的解决方案、从局部性和杠杆角度阐述的收益、前后对比图，以及一个 `Strong`（强）/ `Worth exploring`（值得探索）/ `Speculative`（推测性）徽章。报告的结尾会给出它自己会最先动手的那个。

然后它会停下来，问你想探索哪一个。选定之后，它会针对那个设计运行 [grilling](https://aihero.dev/skills-grilling) 循环——约束条件、接缝后面藏着什么、哪些测试能存活下来——随着决策逐渐清晰，内联地更新领域模型。

## 它在流程中的位置

`improve-codebase-architecture` 是**周期性维护**——每隔几天运行一次，而不是流程链条中的一环。它的近邻有：[codebase-design](https://aihero.dev/skills-codebase-design)，它拥有每个候选项写作时所用的"深度与接缝"词汇体系；[grilling](https://aihero.dev/skills-grilling)，在你选定候选之后走完决策树；以及 [domain-modeling](https://aihero.dev/skills-domain-modeling)，在重设计尘埃落定时保持 `CONTEXT.md` 和 ADR 的更新。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
