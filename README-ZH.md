<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 为真正的工程师准备的技能（Skills）

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

这是我每天都在使用的智能体技能，用来做真正的工程 —— 而不是靠感觉编程（vibe coding）。

开发真实的应用程序很难。像 GSD、BMAD 和 Spec-Kit 这类方法试图通过「接管整个流程」来帮忙。但这样做的同时，它们夺走了你的控制权，让流程中出现的 bug 难以解决。

这些技能被设计为**小巧、易于改造、可组合**。它们适用于任何模型。它们基于数十年的工程经验。随意折腾它们，把它们变成你自己的东西，尽情享用。

如果你想跟进这些技能的更新，以及我之后创建的新技能，你可以加入我的 newsletter，和约 60,000 名其他开发者一起：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 快速上手（30 秒完成设置）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的技能，以及你想把它们安装到哪些编程智能体上。**请务必选择 `/setup-matt-pocock-skills`**。
3. 在你的智能体中运行 `/setup-matt-pocock-skills`。它会：

   - 询问你想使用哪个 issue 跟踪器（GitHub、Linear 或本地文件）
   - 询问你在分拣（triage）工单时会打上哪些标签（`/triage` 会用到标签）
   - 询问你想把我们创建的文档保存在哪里
4. 搞定 —— 你可以开始使用了。

## 作为 Claude Code 插件安装

更喜欢即装即用、不需要手动维护的安装方式？这些技能也以原生 [Claude Code 插件](https://code.claude.com/docs/en/plugins) 的形式发布。插件不是把可编辑的文件复制到你的仓库里，而是把整套技能作为一个受管理的包来安装，我发布新版本时会自动更新 —— 你是「订阅」而不是「fork」。

在 Claude Code 中：

```
/plugin marketplace add mattpocock/skills
/plugin install mattpocock-skills@mattpocock
```

或在终端中：

```bash
claude plugin marketplace add mattpocock/skills
claude plugin install mattpocock-skills@mattpocock
```

然后像上面快速上手里那样，每个仓库运行一次 `/setup-matt-pocock-skills`。

两种安装方式，两种理念：

- **[skills.sh](https://skills.sh/mattpocock/skills)** 会把技能复制到你的项目中，方便你魔改，把它们变成你自己的东西。
- **插件**则把它们保持为一个只读、永远最新的包，你不用去编辑 —— 适合那种只想让我这套技能开箱即用、并跟随它一起演进的情况。

> 在用 Codex 或其他智能体？[skills.sh 安装器](https://skills.sh/mattpocock/skills) 现在就能把这些技能安装进 Codex 以及其他遵循 Agent-Skills 标准的工具。原生 Codex 插件已在路线图上 —— 见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

## 为什么要有这些技能

我构建这些技能，是为了修复我在 Claude Code、Codex 以及其他编程智能体身上看到的常见失效模式。

### 问题 #1：智能体没做我想要的

> "没有人确切知道自己想要什么"
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》（The Pragmatic Programmer）

**问题所在**。软件开发中最常见的失效模式是**错位（misalignment）**。你以为开发者懂了你的意思。然后你看到他做出来的东西 —— 才意识到他根本没理解你。

在 AI 时代也一样。你和智能体之间存在一条沟通鸿沟。修复它的办法是一场**拷问式对话（grilling session）** —— 让智能体就你要做的东西向你追问各种细节。

**修复方法**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) - 用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) - 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但加了更多好东西（见下文）

这是我最受欢迎的两个技能。它们帮你在动手之前先和智能体对齐，并深入思考你要做的改动。**每次**你想做改动时都用它们。

### 问题 #2：智能体太啰嗦了

> 借助通用语言（ubiquitous language），开发者之间的对话以及代码的表达，都源自同一个领域模型。
>
> Eric Evans，《[领域驱动设计](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》（Domain-Driven Design）

**问题所在**：在项目刚起步时，开发者与他们为之构建软件的人（领域专家）通常说着不同的语言。

我和我的智能体之间也感受到了同样的张力。智能体通常是被丢进一个项目里，被要求边干边摸索行话。于是它们用 20 个词来表达 1 个词就能搞定的事。

**修复方法**是一套共享语言。它是一份文档，帮助智能体解读项目里使用的行话。

<details>
<summary>
示例
</summary>

这是我的 `course-video-manager` 仓库里的一份 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪个更易读？

- **之前**：「当课程某个章节里的一节课被『落地』时（也就是在文件系统里被分配一个位置），会出一个问题」
- **之后**：「materialization cascade（物化级联）有个问题」

这种简洁性在一个又一个会话中持续带来回报。

</details>

这已经内置在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 中。它是一场拷问式对话，但它能帮你和 AI 建立共享语言，并把难以解释的决定记录在 ADR 里。

很难用语言形容这有多强大。它可能是这个仓库里最酷的一项技术。试一试，你就知道了。

> [!TIP]
> 共享语言除了能减少啰嗦，还有很多其他好处：
>
> - **变量、函数和文件会一致地使用共享语言来命名**
> - 结果是，**智能体更容易浏览代码库**
> - 智能体在**思考时消耗的 token 也更少**，因为它能用更简洁的语言

### 问题 #3：代码跑不起来

> "永远迈出小而审慎的步子。反馈的速度就是你的速度上限。永远不要承担太大的任务。"
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题所在**：假设你和智能体已经对要做什么达成一致。如果它*还是*做出一堆垃圾，怎么办？

是时候看看你的反馈回路了。如果得不到「代码实际运行效果如何」的反馈，智能体就是在盲飞。

**修复方法**：你需要常规的一整套反馈回路：静态类型、浏览器访问、以及自动化测试。

对于自动化测试，红-绿-重构（red-green-refactor）循环至关重要。也就是智能体先写一个失败的测试，然后再修复它。这能给智能体一个稳定的反馈水平，从而产出好得多的代码。

我构建了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 技能**，可以插进任何项目里。它鼓励红-绿-重构，并为智能体提供大量关于「什么是好测试、什么是坏测试」的指导。

至于调试，我还构建了一个 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** 技能，把调试最佳实践包装成一个简单的循环。

### 问题 #4：我们建出了一团乱麻

> "*每天*都要在系统设计上投入。"
>
> Kent Beck，《[解析极限编程](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》（Extreme Programming Explained）

> "最好的模块是『深』的。它们让大量功能通过一个简单的接口就能被访问。"
>
> John Ousterhout，《[软件设计哲学](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》（A Philosophy of Software Design）

**问题所在**：用智能体构建的大多数应用都复杂且难以修改。因为智能体能极大加速编码，它们也加速了软件熵增。代码库正以前所未有的速度变得更复杂。

**修复方法**是一种全新的、由 AI 驱动的开发方式：关心代码的设计。

这已经内置进这些技能的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 会在创建规格说明之前，先询问你要改动哪些模块

而最关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 能帮你拯救一个已经变成一团乱麻的代码库。我建议每隔几天就在你的代码库上跑一次。

### 小结

软件工程基本功比以往任何时候都更重要。这些技能是我把基本功浓缩成可重复实践的最大努力，帮你交付职业生涯中最好的应用。尽情享用。

## 参考手册

这些技能只按一个维度来划分 —— 谁能调用它们。**用户调用（User-invoked）**的技能只能在你手动输入时触发（比如 `/grill-me`）；它们的职责是编排。**模型调用（Model-invoked）**的技能可以由你调用，*也可以*在任务匹配时由智能体自动取用；它们承载的是可复用的纪律。一个用户调用的技能可以去调用模型调用的技能，但绝不能调用另一个用户调用的技能。

### 工程（Engineering）

我每天用于代码工作的技能。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** —— 询问哪个技能或流程适合你的情况。这是本仓库中用户调用技能的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** —— 一场拷问式对话，同时还会构建你项目的领域模型，打磨术语，并就地更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** —— 让 issue 在一套分拣角色的状态机中流转。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** —— 扫描代码库，找出可深化的机会，把它们呈现为一份可视化 HTML 报告，然后针对你选中的那一项展开拷问。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** —— 为工程技能配置本仓库（issue 跟踪器、分拣标签、领域文档布局）。在使用其他工程技能前，每个仓库运行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** —— 把当前对话转化为一份规格说明，并发布到 issue 跟踪器。不做访谈 —— 只是把你们已经讨论过的内容综合起来。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** —— 把任何计划、规格或对话拆解成一组 tracer-bullet 工单，每张工单都声明自己的阻塞依赖 —— 可以作为文本写在本地文件里，或作为真实跟踪器上的原生阻塞链接。
- **[implement](./skills/engineering/implement/SKILL.md)** —— 构建规格或一组工单所描述的工作，在预先约定的接缝处驱动 `/tdd`，并在提交前用 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** —— 规划一大块工作（大到单个智能体会话装不下），把它变成 issue 跟踪器上一张共享的调查工单地图 —— 一次解决一张，直到通往目标的路径清晰为止。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)** —— 构建一个一次性的原型来回答设计问题 —— 回答状态/逻辑问题时是一个可运行的终端应用，回答 UI 问题时是几个截然不同、可从一个路由切换的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** —— 针对难缠 bug 和性能回退的纪律化诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** —— 针对高可信的一手来源调查一个问题，并把结论作为一份带引用的 Markdown 文件捕获到仓库里，以后台智能体的方式运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** —— 采用红-绿-重构循环的测试驱动开发。一次一个垂直切片地构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** —— 主动构建并打磨项目的领域模型 —— 用术语表来校验术语，用边界场景做压力测试，并就地更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** —— 设计深模块的共享纪律和词汇表：在一个小接口背后承载大量行为，放在干净的接缝处，并能通过那个接口进行测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)** —— 对自某个固定点以来的 diff 做两轴评审：**规范**（是否遵循仓库的编码规范，外加 Fowler 坏味道基线？）和**规格**（是否忠实地实现了原始 issue/PRD？），以并行子智能体的方式运行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)** —— 逐块（hunk）处理进行中的 git merge 或 rebase 冲突，通过追溯到每一侧一手来源的意图来消解，然后完成这次操作 —— 绝不 `--abort`。

### 生产力（Productivity）

通用的工作流工具，不针对具体代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** —— 针对一个计划或设计被无情地盘问，直到决策树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** —— 把当前对话压缩成一份交接文档，好让另一个智能体接续这项工作。
- **[teach](./skills/productivity/teach/SKILL.md)** —— 跨多个会话教用户一项新技能或新概念，把当前目录用作一个有状态的教学工作区。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** —— 关于如何写好、编辑好技能的参考：让一个技能变得可预测的词汇表和原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** —— 针对一个计划、决定或想法无情地盘问用户，直到决策树的每个分支都被解决。这是 `grill-me` 和 `grill-with-docs` 背后可复用的循环。
