快速开始：

```bash
npx skills add mattpocock/skills --skill=wayfinder
```

```bash
npx skills update wayfinder
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder)

## 它的作用

`wayfinder` 处理那些大到单个 agent 会话装不下的工作——它被迷雾笼罩，从这里到目标的路径还看不清楚——它会在你的 issue 追踪器上把这项工作绘制成一张由**决策工单（decision tickets）**组成的**共享地图**，然后逐一解决这些工单，直到前路清晰。它**只做规划，不做实现**：每张工单解决的都是一个决策——一个需要敲定的*问题*，而不是一段要执行的构建任务——当"在有人动手构建之前再没有什么需要决定"时，这张地图就完成了——所以它产出的是决策，而不是交付物。

## 什么时候用它

你可以通过输入 `/wayfinder` 来调用它——agent 不会自己主动使用它。

当一项工作**超出单个 agent 会话的容量**，且通往**目的地**的路线仍然迷雾重重时——你能感觉到这项工作的轮廓，但还没法把它写成规格（spec）或计划——就该用它了。要把一段*已经清晰的*脉络转变成规格，请使用 [to-spec](https://aihero.dev/skills-to-spec)；要把一份已经被理解的计划切分成可构建的工单，请使用 [to-tickets](https://aihero.dev/skills-to-tickets)。wayfinder 位于两者的上游：当迷雾太浓、无法直接写规格时，就是你该运行它的时候。

## 前置条件

地图和它的工单都存放在仓库的 issue 追踪器上，因此 wayfinder 需要 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 所铺设的追踪器配置——它会写入一节"Wayfinding operations（探路操作）"，说明对于 GitHub、GitLab 或本地 Markdown，地图、子工单、阻塞关系和边界（frontier）查询分别如何表达。如果缺少这份文档，wayfinder 会默认使用本地 Markdown 地图。

## 地图是索引，迷雾是边界

**地图**是一个单独的 `wayfinder:map` issue，它的工单就是这个 issue 的子 issue——整个团队可以共同关注同一个 URL。它是一个**索引，而不是存储**：每个决策恰好只存在于一个地方（它自己的工单），地图只做摘要和链接，绝不复述内容。会话以低分辨率加载地图，按需放大到单个工单。

在活跃工单之外是**战争迷雾（fog of war）**——你能感觉到即将到来、但还无法锁定的决策。判断某样东西是工单还是迷雾的标准，是你现在能否*精确地陈述这个问题*，而不是能否回答它。解决一张工单会清除它前方的迷雾，把现在可以明确表述的内容**毕业（graduating）**为新的工单。**边界（frontier）**是那些开放的、未被阻塞的、无人认领的工单——已知的边缘——追踪器原生的阻塞关系会把它直观地渲染出来，所以你不用打开地图就能看到哪些工单可以认领。迷雾只朝**目的地**的方向聚集；越过目的地的工作被裁定为**超出范围（out of scope）**，直接关闭，永不毕业。

每张工单要么是 **HITL**（human in the loop，人在环路——追问、原型），要么是 **AFK**（agent 独自完成——调研）；HITL 工单只能通过实时交流来解决，所以 agent 绝不会自问自答。调研工单依然是一张真正的工单——一个下游决策所依赖的共享阻塞点——但因为它是 AFK 的，会话不会停下来慢慢读：它会启动一个 `/research` **子 agent** 来并行地消耗这张工单，保持边界快速推进，并把调研结论记录在一个一次性的 `research/<name>` 分支上。

## 如何判断它工作正常

- 命名**目的地**是第一个动作——在任何工单存在之前——因为它确定了每张工单都要对照衡量的范围。
- 一张地图就是一个 `wayfinder:map` issue；工单是它的子 issue，通过**名称**引用，绝不使用裸的 `#42`。
- 一个会话**最多解决一张工单**（调研工单除外），把答案记录为一条解决评论，关闭工单，并在 *Decisions so far（至今的决策）* 中追加一行指针。
- 如果开场的追问没有发现**任何迷雾**，它会停下来告诉你：这段旅程足够小，可以跳过地图。

## 它在流程中的位置

`wayfinder` 是一个大想法的**入口匝道（on-ramp）**：一项太大、太模糊、无法一次写完规格的工作，会生成一张被清理完毕的决策地图，然后并入主构建流程。当迷雾被推开、前路清晰时，交给 [to-spec](https://aihero.dev/skills-to-spec) 来安排多会话的构建（或者，如果这项工作最后发现很小，就直接实现）。它依靠 [grilling](https://aihero.dev/skills-grilling) 和 [domain-modeling](https://aihero.dev/skills-domain-modeling) 来解决单个工单，依靠 [prototype](https://aihero.dev/skills-prototype) 和 [research](https://aihero.dev/skills-research) 来处理需要它们的工单类型。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
