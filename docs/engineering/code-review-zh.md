快速开始：

```bash
npx skills add mattpocock/skills --skill=code-review
```

```bash
npx skills update code-review
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review)

## 它的作用

`code-review` 审查的是 `HEAD` 与你提供的某个固定点之间的 diff——这个固定点可以是一个 commit、分支、tag 或 merge-base——审查沿着两条相互独立的轴展开：**规范**（代码是否遵循本仓库记录在案的约定？）和**规格**（代码是否实现了原始 issue 或 spec 所要求的内容？）。每条轴都以各自独立的并行子 agent 运行，并并排汇报结果。它从不会把两组发现合并或重新排序——让它们保持分离正是这个 skill 的核心意义，因为一个改动可能在一轴上通过却在另一轴上失败，而单一的混合结论会让其中一方掩盖另一方。

## 什么时候用它

输入 `/code-review` 即可调用，或者当你要求审查一个分支、一个 PR、进行中的改动、或任何"自 X 以来"的内容时，agent 会自动使用它。

当存在一个可以对照已知良好基准点来判断的 diff，并且你希望两个问题——*它构建得对吗？*和*它构建的是对的东西吗？*——被各自独立地回答时，就该用它了。它运行在构建循环的末尾；如果要真正以测试先行的方式写代码，请使用 [tdd](https://aihero.dev/skills-tdd)；如果要把一整份规格构建成代码，请使用 [implement](https://aihero.dev/skills-implement)，它会在提交前自己运行一轮 `/code-review`。

## 前置条件

**规格**轴需要有地方能找到原始规格——commit 信息中的 issue 引用、你传入的路径、或 `docs/`/`specs/` 目录下的某份 spec。这套 issue 追踪器的接线来自 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills)；如果找不到规格，规格轴会直接跳过并明说。**规范**轴不需要任何配置——即使仓库里没有任何记录在案的约定，它也始终自带一套 Fowler 代码异味基线。

## 两条轴，永不合并

这个 skill 的定义性理念就是**两条轴**。**规范**轴询问的是：这个 diff 是否符合本仓库写代码的方式——即它的 `CODING_STANDARDS.md` 或 `CONTRIBUTING.md`，外加一套固定的约 12 条 Fowler 代码异味基线（神秘命名、重复代码、依恋情结、数据泥团……）。有两条规则保证这套基线的安全性：记录在案的仓库规范永远优先于基线，且每条异味都只是一个判断提示，绝不是硬性违规。**规格**轴问的是正交的问题——代码是否做到了 issue 或 spec 真正要求的事情，既没有遗漏需求，也没有夹带范围蔓延？

它们以并行子 agent 的方式运行，这样任何一方的上下文都不会污染另一方，最终报告把它们呈现在各自独立的 `## Standards` 和 `## Spec` 标题下，并附上每轴的小结。这里刻意不存在一个跨轴的单一赢家。

## 如何判断它工作正常

- 它会先固定并确认那个基准点（`git rev-parse`），遇到无效引用或空 diff 时快速失败，而不是让子 agent 跑到一半才出错。
- 规范与规格的发现以两个不同的区块呈现，各自注明出处——一边是仓库规范或基线异味，另一边是被引用的 spec 原文。
- 当找不到任何规格时，规格轴会报告"没有可用规格"，而不是凭空编造需求。

## 它在流程中的位置

`code-review` 是主构建链末端的审查步骤：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它最近的邻居是 [implement](https://aihero.dev/skills-implement)——后者驱动整个构建过程，并在提交前调用本 skill 作为自己的审查环节；往上游看，它所对照的规格由 [to-spec](https://aihero.dev/skills-to-spec) 和 [to-tickets](https://aihero.dev/skills-to-tickets) 产出。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
