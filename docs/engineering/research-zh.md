快速开始：

```bash
npx skills add mattpocock/skills --skill=research
```

```bash
npx skills update research
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/research)

## 它的作用

`research` 通过阅读真正拥有答案的那些来源来回答问题，并留下一份带引用的 Markdown 文件。它只使用**一手来源**——官方文档、源代码、规范、第一方 API——绝不使用对它们的二手转述，所以它保存下来的内容可以一直追溯到权威出处，而不是一份摘要的摘要。

## 什么时候用它

输入 `/research` 调用它，或者当任务变成阅读的苦差事时，agent 会自动用上它。

当下一步是*弄清某件事*——一个 API 的行为、一份规范到底说了什么、某个说法是否成立——而你又不想让自己手头的工作线程停下来做阅读时，就该用它了。如果你想通过访谈而不是阅读来打磨计划，用 [grilling](https://aihero.dev/skills-grilling)；想写点用完即弃的代码来探索要构建什么，用 [prototype](https://aihero.dev/skills-prototype)。

## 外包出去的跑腿活

它的核心动作是：阅读过程作为一个**后台 agent** 运行。你继续工作；它跑出去，把每个论断一路追到一手来源，然后把一份带引用的 Markdown 文件放进仓库里专门存放这类笔记的地方。研究是你外包出去的跑腿活，而不是你外包出去的思考——你拿到的是一份可以回应的文档，来源都附在上面。

## 它在流程中的位置

它是一个随时可以拿起来用的独立 skill，为各种思考类 skill 供料：它产出的文件是可以拿去 grill、做计划或做设计的东西，所以它处在 [grilling](https://aihero.dev/skills-grilling) 和 [to-prd](https://aihero.dev/skills-to-prd) 这类工作的上游，而不在构建链里。完整的地图见 [ask-matt](https://aihero.dev/skills-ask-matt)。
