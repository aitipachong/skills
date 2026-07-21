快速上手：

```bash
npx skills add mattpocock/skills --skill=grill-me
```

```bash
npx skills update grill-me
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)

## 它是做什么的

`grill-me` 会围绕一个计划或设计展开一场毫不留情的访谈，沿着决策树的每一条分支一路追问，直到你和智能体达成**共识**为止。

它**一次只问一个问题**，然后耐心等待。它绝不会一次性把一堆问题抛给你——那样只会让人不知所措——而且凡是能通过阅读代码库回答的问题，它都会自己去读，而不是来问你。每个问题都会附带智能体自己推荐的答案，所以你是在对一个提案做出反应，而不是对着一个空白的提示框发呆。

## 什么时候该用它

你需要输入 `/grill-me` 来主动调用它——智能体不会自己想起用它。

在动手构建之前，当一个计划感觉大致没问题、但你能察觉到其中还藏着未解决的决策时，就该用它了——正是你想把薄弱环节找出来、逼到台面上的时刻。如果你希望这场拷问同时还能留下一份 ADR（架构决策记录）和术语表的纸质痕迹，那就改用 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)。而如果这项工作大到无法在一次会话中装下、通往目标的路线也仍然迷雾重重——比如一个全新的项目、一个庞大的功能开发——那就从更上游的 [wayfinder](https://aihero.dev/skills-wayfinder) 开始，它会先把整件事绘制成一张决策地图，然后再汇合回这个流程。

## 决策树

整场会话会把计划当作一棵决策树来走，逐个解决决策之间的依赖关系——父决策先敲定，挂在它下面的选择再跟进。重点不在于快速达成一致，而在于让每一个隐含的决定都显式化，不让任何重要的事情被默默假设掉。走完这一遭，你会得到一个所有分支都被造访过的计划。

`grill-me` 是**无状态的**：它不写任何文件，也不留下任何工作区。它可以在任何地方运行，唯一的产物就是对话本身被磨砺出的清晰理解。这正是它与 [grill-with-docs](https://aihero.dev/skills-grill-with-docs) 的刻意区别——后者会把同一场访谈固化为持久的 ADR 和术语表。

## 它在整个体系中的位置

`grill-me` 是一个随时可取用的独立工具——每当一个计划需要加固时，你都可以运行这场构建前的压力测试。它是 [grilling](https://aihero.dev/skills-grilling) 原语的无状态、由用户主动调用的前门；它最近的邻居是 [grill-with-docs](https://aihero.dev/skills-grill-with-docs)，这个有状态的兄弟会运行同样的访谈，但额外把决策记录为 ADR 和术语表。如果你想要的成果是一份落在纸面上的规格说明，那就交接给 [to-spec](https://aihero.dev/skills-to-spec)，它会把已经敲定的理解综合成一份规格，而不会重新采访你。当你不确定该走哪条流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
