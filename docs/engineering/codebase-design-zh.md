快速开始：

```bash
npx skills add mattpocock/skills --skill=codebase-design
```

```bash
npx skills update codebase-design
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design)

## 它的作用

`codebase-design` 给你一套共享而精确的词汇，用来设计**深模块**——把大量行为藏在一个小接口背后，安放在一条干净的接缝上，并且能通过那个接口被测试。

它是**一门语言，而不是一套流程**。它不会替你重构代码，也不会交给你一份重构计划——它修正的是用词（模块、接口、深度、接缝、适配器、杠杆、局部性），好让每一场设计讨论、以及每一个触及设计的其他 skill，都用同一种方式说话。一致的语言就是它的全部意义；"component"、"service"、"API"、"boundary" 这些词被刻意禁用，因为它们会模糊那些真正重要的区分。

## 什么时候用它

输入 `/codebase-design` 调用它，或者当任务契合时 agent 会自动选用它。

当你正在设计或改进一个模块的接口、寻找加深模块的机会、决定接缝该划在哪里，或想让代码更可测、更易于 AI 导航时，就用它。其他 skill 在需要深模块词汇时也会把它拉进来。如果你想打磨的是项目的*领域*术语而非模块设计，请改用 [domain-modeling](https://aihero.dev/skills-domain-modeling)；如果想对现有代码库做一整轮架构梳理，用 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。

## 要深，不要浅

当一个模块把大量行为藏在一个小接口背后时，它就是**深**的；当接口几乎和实现一样复杂时，它就是**浅**的。深度用**杠杆**来衡量——调用方（或测试）每学习一单位接口，能驱动多少行为。关键在于，深度是*接口*的属性，而不是实现的属性：一个深模块内部可以由许多小巧、可替换的部件组合而成，只是这些部件从不暴露给调用方。

有两个检查能解决大部分问题。**删除测试**：想象把这个模块删掉——如果复杂性随之消失，那它只是个传声筒；如果复杂性在 N 个调用方身上重新冒出来，那它确实在创造价值。还有**一个适配器意味着假想的接缝，两个适配器才意味着真实的接缝**——在接缝两侧真的有东西变化之前，不要急着切出接缝。

## 接口就是测试面

调用方和测试跨过的是同一条接缝，所以一个安放得当的接口，能给测试提供一个耐久的瞄准点，同时接口之下的代码可以自由变动。这就是为什么这套词汇坚持用**接缝**（seam，Feathers 的术语——一个你无需修改该处代码就能改变行为的地方），而不用被过度负载的 "boundary"；也是为什么这里的 "接口" 指的是*调用方必须知道的一切事实*：签名当然算，但还包括不变量、顺序、错误模式和性能——而不只是类型层面的表面。

## 有意拆出来的原因

`codebase-design` 是深模块词汇的**唯一权威来源**，被刻意拆成一个独立的、可被模型调用的 skill，好让任何东西都能触达它。其他 skill 指向它，而不是重述这些词：[tdd](https://aihero.dev/skills-tdd) 借用它在写测试之前安放接缝，[improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture) 在重构现有代码时倚靠它，[to-spec](https://aihero.dev/skills-to-spec) 在写规格之前勾勒接缝和加深机会时说的也是这套语言。

让它保持独立的意义在于，你也可以单独取用——把它当作一份关于如何思考模块设计的**参考**——而不必触发那些 skill 所规定的更大流程。把词汇在一个地方修正一次，之后每一场设计讨论都能继承它们。

## 它在流程中的位置

`codebase-design` 是一个**随时可取用的独立 skill**——是工程类 skill 之下的共享词汇层。它最亲近的邻居是 [domain-modeling](https://aihero.dev/skills-domain-modeling)，那是与它平行的词汇 skill，面向问题领域而非模块结构。当你不确定哪个 skill 或流程合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
