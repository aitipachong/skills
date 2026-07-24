快速上手：

```bash
npx skills add mattpocock/skills --skill=implement
```

```bash
npx skills update implement
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement)

## 它做什么

`implement` 负责把 spec（规格说明）或一组 ticket（工单）中描述的工作真正构建出来 —— 以测试驱动开发、类型检查和完整测试套件来推进，然后交接给代码审查，并提交到当前分支。

它**不**负责决定要构建什么。spec 已经定稿，接缝（seam）也已经达成一致；`implement` 是执行这个计划，而不是重新打开它。它是手，而不是脑 —— 思考早已在上游完成。

## 什么时候用它

你需要通过输入 `/implement` 来调用它 —— agent 不会主动使用它。

当工作已经写成 spec 或拆分成 ticket、你准备把它变成代码时，就用它。如果 spec 还不存在，先写 spec —— 可以用 [to-spec](https://aihero.dev/skills-to-spec)，或者用 [to-tickets](https://aihero.dev/skills-to-tickets) 把 spec 拆成 ticket。如果你只是想在没有完整 spec 的情况下以测试先行的方式构建东西，直接使用 [tdd](https://aihero.dev/skills-tdd)。

## 预先约定的接缝

`implement` 赖以运转的核心概念是**接缝（seam）**—— 在写任何代码之前就选定的、用于测试某个功能的稳定接口。它不会在构建过程中临时发明接缝；它使用已经选好的接缝（在 [to-spec](https://aihero.dev/skills-to-spec) 阶段），并通过 [tdd](https://aihero.dev/skills-tdd) 针对这些接缝编写测试。在预先约定的接缝上工作，是实现保持诚实的关键：测试针对的是持久不变的东西，因此底层代码可以变动，而测试不必跟着动。

围绕这个核心，它保持紧凑的循环 —— 频繁做类型检查，边做边跑单个测试文件，最后跑一遍完整测试套件 —— 然后以一轮审查和一次提交到当前分支收尾。

## 它在流程中的位置

`implement` 是主链路中靠近末尾的构建步骤，就在审查之前：

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

在工作已经写好 spec 并排好顺序之后再使用它，而不是在此之前。它最重要的邻居是 [to-tickets](https://aihero.dev/skills-to-tickets) —— 它产出的 ticket（每个都声明了自己的阻塞依赖边）正是 `implement` 逐一处理的对象；以及 [tdd](https://aihero.dev/skills-tdd) —— `implement` 在内部驱动它在每个接缝处先写测试，然后再运行自己的 [code-review](https://aihero.dev/skills-code-review) 审查并提交。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
