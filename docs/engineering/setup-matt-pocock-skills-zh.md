快速开始：

```bash
npx skills add mattpocock/skills --skill=setup-matt-pocock-skills
```

```bash
npx skills update setup-matt-pocock-skills
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills)

## 它的作用

`setup-matt-pocock-skills` 教会一个仓库：工程类 skill 在其中应该如何运作——issue 放在哪里、分诊标签叫什么、领域文档（domain docs）放在哪里——并把这些答案记录为其他 skill 会读取的**配置**。

它写的是配置，而不是把行为硬编码进去。工程技能链假定 `docs/agents/` 下存在三个文件；这个 skill 就是产生它们的一次性引导程序——它从你真实的仓库中发现答案（`git remote`、已有的标签、已有的 `CONTEXT.md`），并与你确认，而不是靠猜。它是提示词驱动的——先探索、展示发现、确认，然后才写文件——而不是一个确定性的脚手架。

## 什么时候用它

你通过输入 `/setup-matt-pocock-skills` 来调用它——agent 不会自己主动使用它。

**每个仓库一次，在任何其他工程类 skill 首次使用之前**运行它。如果 [triage](https://aihero.dev/skills-triage)、[to-spec](https://aihero.dev/skills-to-spec) 或 [to-tickets](https://aihero.dev/skills-to-tickets) 开始猜测你的 issue 放在哪里、或者打上你仓库里不存在的标签，那说明这里还没做过 setup。只有当你想更换 issue 追踪器或从头再来时才需要重新运行——日常的微调就是直接编辑 `docs/agents/*.md`。

## 三个决策

每个决策它都会先给出一个推荐答案，你一句话就能接受；凡是它已经能推断出来的部分都会跳过——所以大多数运行只是几下快速确认：

- **Issue 追踪器**——工作在哪里被跟踪，这样 `triage`/`to-spec`/`to-tickets` 才知道该调用 `gh`、`glab`、往 `.scratch/` 下写 markdown，还是遵循你描述的工作流。GitHub、GitLab、本地 markdown，或其他。（它会推荐与你的 `git remote` 匹配的那个。）
- **分诊标签**——仅在安装了 `triage` skill 时才会问，而且只问一句：保留默认标签（`needs-triage`、`needs-info`、`ready-for-agent`、`ready-for-human`、`wontfix`）吗？只有当你的追踪器已经在用别的名字时才说否，这样 `triage` 打的是真实存在的标签，而不是创建重复标签。
- **领域文档**——默认假定单上下文（根目录一个 `CONTEXT.md` + `docs/adr/`），这几乎适合所有仓库；只有当它发现 monorepo 信号时，才会提出多上下文映射的方案。

产出是 `docs/agents/` 下的一组文件——`issue-tracker.md`、`domain.md`，以及当安装了 `triage` 时的 `triage-labels.md`——外加在仓库已有的 `CLAUDE.md` / `AGENTS.md` 中追加一个指向它们的 `## Agent skills` 区块。这些文件就是整个工具包其余部分所依赖的共享基座。

## 如何判断它工作正常

- `issue-tracker.md` 和 `domain.md` 落在 `docs/agents/` 下（安装了 `triage` 时还有 `triage-labels.md`），并且你的 `CLAUDE.md` 或 `AGENTS.md` 中出现了 `## Agent skills` 一节。
- 它推荐的追踪器与你真实的 `git remote` 一致，标签与你仓库中已存在的字符串一致。
- 之后，`triage` 和 `to-tickets` 会用正确的标签作用于正确的地方，而不是再来问你或靠猜。

## 它在流程中的位置

`setup-matt-pocock-skills` 是一次**一次性的 setup**——整个工程技能集所依赖的地基，而不是一个要重复执行的步骤。它的近邻是那些读取它所写配置的 skill：[triage](https://aihero.dev/skills-triage)，因为它使用这里配置的标签词汇；以及 [to-spec](https://aihero.dev/skills-to-spec) / [to-tickets](https://aihero.dev/skills-to-tickets)，因为它们会把内容发布到这里配置的 issue 追踪器中。先运行它；下游的一切都假定它已经运行过了。当你不确定该用哪个 skill 或流程时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
