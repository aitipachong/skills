快速开始：

```bash
npx skills add mattpocock/skills --skill=to-tickets
```

```bash
npx skills update to-tickets
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets)

## 它的作用

`to-tickets` 把一份计划、一份 spec、或者当前对话拆成一组 **ticket**——每个 ticket 都是一枚"曳光弹"式的垂直切片——并把它们发布到你配置好的追踪器中，每个 ticket 都会声明阻塞它的其他 ticket。

每个 ticket 都是一枚**曳光弹（tracer bullet）**——一条端到端贯穿所有集成层（schema、API、UI、测试）的*垂直*细切片，而绝不是某一层的水平切片。一个完成的切片可以独立演示或验证，这正是每个 ticket 能放心交给 agent 去做的原因。

## 什么时候用它

你通过输入 `/to-tickets` 来调用它——agent 不会自己主动使用它。

等你们已经有了一份达成共识的计划或一份写好的 spec、想把它拆成 ticket 时，就该用它了。你可以直接让它基于当前对话来拆，也可以传一个 spec 或 issue 引用给它，它会先把正文和评论抓下来。如果这个改动还没写成 spec，先产出一份——这一步用 [to-spec](https://aihero.dev/skills-to-spec)。

## 前置条件

`to-tickets` 会发布到你的 issue 追踪器，所以必须先用 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 为这个仓库配置好追踪器及其分诊标签体系。在真实的追踪器上，它会在发布时打上 ready-for-agent 标签。

## 一份产物，两种读法

阻塞边（blocking edge）才是整个拆分的重点。它们让同一组 ticket 有两种读法，取决于追踪器：

- **本地文件** → 每个 ticket 一个文件，放在 `.scratch/<feature>/issues/` 下，按阻塞者优先编号，阻塞边以文字形式写明。你自上而下逐个手动处理，全程保持在环。
- **真实追踪器（GitHub、Linear）** → 每个 ticket 一个 issue，阻塞边以原生的阻塞链接（或子 issue）表示。任何阻塞项全部完成的 ticket 都处在**前沿（frontier）**上，可以直接认领——所以多个 agent 可以同时开工。

无论载体是什么，阻塞边都存在于 ticket 里；载体只决定是否有东西能并行地作用于它们。`to-tickets` 负责产出这份产物——怎么跑它（手动串行，还是并行舰队）由你决定。

## 垂直切片，而非水平切片

整个 skill 的关键就在于这一个区分。**水平**切片交付的是改动的某一层——全部 schema，或全部 API——在所有层落地之前，什么都跑不起来。**垂直**切片，也就是曳光弹，一次交付一条贯穿*每一层*的窄路径，所以它一做完就能演示。

在切片之前，`to-tickets` 会先寻找预重构（prefactoring）的机会——"先让改动变得容易，再去做这个容易的改动"——并把这类工作排在最前。然后它会就拆分方案向你提问（粒度、阻塞边、哪些该合并哪些该再拆），确认后才发布，并且按阻塞者优先的顺序发布，这样每个 ticket 的"Blocked by"都能引用到真实存在的 ticket。

## 宽重构的例外

有一种形状会打破曳光弹规则：**宽重构（wide refactor）**——一次机械性改动（重命名一个列、改一个共享符号的类型），其**爆炸半径**蔓延到整个代码库，于是一次编辑同时弄坏上千个调用点，任何垂直切片都不可能单独变绿。`to-tickets` 会改用**扩张–收缩（expand–contract）**的方式来切：先扩张（让新形态与旧形态并存，什么都不破坏），再迁移（按爆炸半径决定批次大小，把调用点分批迁过去，每批一个 ticket，全程 CI 保持绿色，因为旧形态还在），最后收缩（等没有任何调用者时再删除旧形态）。如果连各批次都无法单独保持绿色，它们就共享一条集成分支，共同阻塞一个最终的集成验证 ticket，绿色只在那个 ticket 上兑现。

## 它在流程中的位置

`to-tickets` 是主构建链中的一步：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它位于 [to-spec](https://aihero.dev/skills-to-spec)（交给它一份已敲定的 spec，里面有可供切片的用户故事）和 [implement](https://aihero.dev/skills-implement)（负责构建每个 ticket，内部驱动 [tdd](https://aihero.dev/skills-tdd) 以测试先行，然后过一遍 [code-review](https://aihero.dev/skills-code-review)）之间。沿着前沿逐个领取 ticket 来做，每个 ticket 开一个新的上下文，做完一个清一个。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
