# 生产力工具

通用工作流工具，与代码无关。

## 用户调用型

只有当你手动输入时才能触达（Claude Code：`disable-model-invocation: true`；Codex：在 `agents/openai.yaml` 中设置 `policy.allow_implicit_invocation: false`）。

- **[grill-me](./grill-me/SKILL.md)** — 围绕一个计划或设计对你进行不留情面的访谈，直到决策树的每个分支都被解决。
- **[handoff](./handoff/SKILL.md)** — 把当前对话压缩成一份交接文档，让另一个代理可以接续这项工作。
- **[teach](./teach/SKILL.md)** — 跨多个会话教用户一项新技能或新概念，把当前目录用作有状态的教学工作区。
- **[writing-great-skills](./writing-great-skills/SKILL.md)** — 关于如何写好、改好 skill 的参考：让 skill 可预测的词汇与原则。

## 模型调用型

模型或用户均可触达（带有丰富的触发措辞，方便模型主动取用）。

- **[grilling](./grilling/SKILL.md)** — 围绕一个计划、决策或想法对用户进行不留情面的访谈，直到决策树的每个分支都被解决。
