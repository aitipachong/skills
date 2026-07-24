快速上手：

```bash
npx skills add mattpocock/skills --skill=diagnosing-bugs
```

```bash
npx skills update diagnosing-bugs
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs)

## 它做什么

`diagnosing-bugs` 为棘手的 bug 和性能回归运行一套纪律严明的诊断循环 —— 构建复现、最小化复现、给假设排序、插桩，然后带着回归测试完成修复。

在你拥有**紧凑反馈循环**之前，它拒绝做任何假设 —— 所谓紧凑反馈循环，就是一条已经能在*这个* bug 上变红的可运行命令。在这条命令存在之前，靠读代码来构建理论，正是这个 skill 要阻止的那种失败。没有能变红的循环，就没有诊断。

## 什么时候用它

输入 `/diagnosing-bugs`，或者当任务合适时 agent 会自动拿起它 —— 它会在 “diagnose” / “debug this” 时触发，或者当你报告某个东西坏了、抛错、失败或变慢时触发。

把它留给那些难啃的问题：第一眼看不出来的 bug、间歇性出现的 flake（偶发失败）、在两个已知良好状态之间悄悄溜进来的回归。如果只是想随手验证一个设计问题而不是追查缺陷，请改用 [prototype](https://aihero.dev/skills-prototype)。

## 紧凑循环就是这个 skill 的核心

一旦你有了信号，其他一切 —— 二分查找、假设验证、插桩 —— 都只是机械操作。所以这个 skill 把不成比例的精力花在第一阶段：构造一条能驱动实际 bug 代码路径、并断言你所报告的确切症状的通过/失败命令，然后不断**收紧**它，直到它快速、确定、agent 可运行。一个 30 秒还 flaky 的循环跟没有差不多；一个 2 秒且确定性的循环则是调试的超能力。

它给你一架梯子，上面有各种构建这种循环的方法 —— 失败测试、curl 脚本、CLI diff、无头浏览器、重放的 trace、一次性测试脚手架、fuzz 循环、`git bisect run`、差分运行 —— 只有在万不得已时，才用需要人工参与的 bash 脚本。对于非确定性的 bug，目标不是干净的复现，而是**更高的复现率**：循环触发、并行化、施加压力，直到这个 flake 可以被调试。

## 它在生效的标志

- 它在做任何理论推测*之前*就构建并运行了复现命令 —— 并贴出调用方式及其红色输出。
- 循环断言的是你实际报告的症状，而不是旁边的某个失败。
- 假设以一份排好序的、可证伪的清单呈现，在任何一条被验证之前就先给你看。
- 调试插桩带有标记（`[DEBUG-...]`），并在它宣布完成之前被 grep 出来清理干净。

## 它在流程中的位置

`diagnosing-bugs` 是一个随时可以拿起来用的独立 skill —— 一旦有东西坏了你就进入它，一旦修复和回归测试就位你就退出它。当真正的发现是“没有好的接缝可以把这个 bug 锁死”—— 问题出在代码而不是 bug 本身时，它的事后分析会交接给 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。当你不确定哪个 skill 合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
