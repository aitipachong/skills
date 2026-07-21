技能被组织进 `skills/` 下的各个桶（bucket）文件夹：

- `engineering/` —— 日常代码工作
- `productivity/` —— 日常非代码工作流工具
- `misc/` —— 保留但很少使用，不做推广
- `personal/` —— 绑定我自己的环境配置，不做推广
- `in-progress/` —— 尚未准备好发布的草稿
- `deprecated/` —— 已不再使用

`engineering/` 或 `productivity/`（即**已推广（promoted）**桶）中的每个技能，都必须在顶层 `README.md` 中有一条引用，并且在 `.claude-plugin/plugin.json` 的 `skills` 数组中有一个条目（Claude Code 插件发布的恰好就是这整套已推广技能）。`misc/`、`personal/`、`in-progress/` 和 `deprecated/` 中的技能则**两者都不能出现**。

本仓库同时也是它自己的单插件 Claude Code 市场：`.claude-plugin/marketplace.json` 列出了唯一的 `mattpocock-skills` 插件。提升发布版本号时，要让 `.claude-plugin/plugin.json` 的 `version` 与 `package.json` 的保持同步 —— Claude 依据插件的 `version` 来决定已安装用户何时看到更新。改动任一清单文件后，运行 `claude plugin validate . --strict`。至于为什么是 Claude 插件而（暂时）不是 Codex 插件，见 [.agents/adr/0002-ship-as-a-claude-code-plugin.md](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)。

顶层 `README.md` 中的每个技能条目，都必须把技能名链接到它的 `SKILL.md`。

每个桶文件夹都有一个 `README.md`，用一句话描述列出桶内每个技能，并把技能名链接到它的 `SKILL.md`。已推广桶的 `README.md` 和顶层 `README.md` 会把条目分组成 **User-invoked（用户调用）** 和 **Model-invoked（模型调用）**；非推广桶的 `README.md`（`misc/`、`personal/`）使用扁平列表。

`engineering/` 和 `productivity/` 中的技能还有一个面向人类的文档页，位于 `docs/<bucket>/<skill-name>.md`（docs 目录树镜像了 `skills/` 下那两个桶文件夹）。无论哪个桶，发布的 URL 都是 `https://aihero.dev/skills-<skill-name>` —— docs 路径仅仅是仓库内部的组织方式。当你新增、重命名或改变 `engineering/` 或 `productivity/` 中某个技能的行为时，按照 [.agents/writing-docs.md](./.agents/writing-docs.md) 创建或重新同步它的文档页。非推广桶（`misc/`、`personal/`、`in-progress/`、`deprecated/`）中的技能**没有**文档页。

每个 `SKILL.md` 要么是用户调用（在 `agents/openai.yaml` 中设置 `disable-model-invocation: true` 加上 `policy.allow_implicit_invocation: false`，只能由人类触发），要么是模型调用（模型或用户都可触发）。见 [.agents/invocation.md](./.agents/invocation.md)。

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) 是一个路由器，映射了每个用户可达技能以及它们之间的关系。重新同步文档页的那个触发条件同样适用于它：每当你新增、重命名、移除某个用户可达技能，或改变它如何融入各流程时，重新阅读 `ask-matt` 的 `SKILL.md` 并更新它，让这张地图保持准确 —— 一个它从不提及的新技能，或一个它仍在路由过去的过时技能，就是一个在撒谎的路由器。

要把每个技能（重新）链接进本地工具的 skills 目录（`~/.claude/skills`、`~/.agents/skills`），运行 `scripts/link-skills.sh`。每个条目都是指向本仓库的符号链接，所以一次 `git pull` 就能让已安装的技能保持最新；在新增、移除或重命名技能后，重新运行该脚本。
