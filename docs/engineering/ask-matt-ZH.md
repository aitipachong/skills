快速上手：

```bash
npx skills add mattpocock/skills --skill=ask-matt
```

```bash
npx skills update ask-matt
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt)

## 它是做什么的

`ask-matt` 是本仓库所有技能之上的**路由器**。你描述自己当前所处的情境，它告诉你哪个技能或流程最合适，以及应该按什么顺序运行它们。

它**本身不做任何实际工作**。它不会拷问你、不会写规格说明、也不会修复任何东西——它只负责为你**指路**。它的存在首先是为了那些**用户触发型**技能：因为没有任何机制会自动替你触发它们，所以*你*必须自己记得它们的存在，而 `ask-matt` 就是你把这份记忆外包出去的地方。它也会指向那些你可以按名字直接调用的模型触发型技能——`/tdd`、`/diagnosing-bugs`、`/prototype`、`/code-review`，以及两份词汇表参考 `/domain-modeling` 和 `/codebase-design`。它回答的是"该用哪一个、什么时候用"，然后把你交接给真正干活的那个技能。

## 什么时候该用它

你通过输入 `/ask-matt` 来调用它——agent 不会主动去用它。

每当你不确定某种情境该用哪个技能或流程时，就去找它：比如你有一个想法却不知道从何下手；或者面对一堆 bug 报告，不确定是否该交给 `/triage`；又或者两个技能看起来可以互换、你分不清它们的区别。如果你已经知道要用哪个技能，那就跳过路由器，直接调用它。

## 是"流程"，而不只是"技能"

`ask-matt` 给你的核心思考工具是**流程（flow）**——一条*贯穿*多个技能的路径，而不是某一个孤立的技能。大多数工作都沿着一条**主流程**运行（想法 → 交付：拷问 → 规格 → 工单 → 实现 → 评审），有两条**入口匝道（on-ramps）**汇入它（一条用于接收外来 bug 和请求的 triage 通道；一条用于产生新想法的代码库健康通道），其余的都是你按需单独取用的**独立技能**。你问一个问题，它就会把你放到正确的流程、正确的步骤上——而不只是丢给你一个工具。

## 它在整个体系中的位置

`ask-matt` 是**路由器**——一张覆盖整个技能集的独立地图。它是其他每个文档页都会回链到的节点：[ask-matt](https://aihero.dev/skills-ask-matt)，所以它从不身处任何一条链*之中*；它只是指向*每一条*链。从这里出发，你最常落地的两个地方是：主流程的起点 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)，以及用于处理"不是你自己创建的工作"的入口匝道 [triage](https://aihero.dev/skills-triage)。如果连路由器自己的图景都过时了，那么它的[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt)就是那份权威的地图。
