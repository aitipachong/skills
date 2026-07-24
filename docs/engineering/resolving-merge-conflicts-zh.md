快速上手：

```bash
npx skills add mattpocock/skills --skill=resolving-merge-conflicts
```

```bash
npx skills update resolving-merge-conflicts
```

[源码](https://github.com/mattpocock/skills/tree/main/skills/engineering/resolving-merge-conflicts)

## 它做什么

`resolving-merge-conflicts` 会逐个 hunk 地处理进行中的 git merge 或 rebase 冲突，并把整个操作推进到结束 —— 冲突解决、检查通过、提交完成。

它按**意图**来解决冲突，而不是按文本。在动任何一个 hunk 之前，它会先追溯冲突双方各自的**一手来源** —— commit message、PR、原始 issue —— 弄清每一方为什么做这个改动，然后在两边意图兼容的地方把两边都保留下来。它绝不会为了掩盖冲突而发明新的行为，也绝不会伸手去用 `--abort`：merge 一定要被完成。

## 什么时候用它

输入 `/resolving-merge-conflicts`，或者当任务合适时 agent 会自动拿起它。

当你正处在 merge 或 rebase 中途、git 停在了它自己解决不了的冲突上时，就该用它。它针对的是眼前这个冲突 —— 不是用来规划 merge，也不是用来调试 merge 之后才坏掉的行为。如果 merge 已经完成、但有些东西莫名其妙地开始失败，请改用 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)。

## 按意图解决冲突

冲突中最常见的陷阱是把它当成一个文本问题 —— 为了让冲突标记消失而选 “ours” 或 “theirs”。这个 skill 把它当作一个**意图**问题。hunk 的每一侧之所以存在，是因为有人想要某个东西；解决方案必须在可能的情况下同时尊重两边的诉求，而在两边确实互不兼容的地方，选择那个与这次 merge 既定目标一致的一方，并大声说明这个取舍。

这就是一手来源如此重要的原因。你不可能保留一个你没有读过的意图，所以工作要从历史记录开始 —— commit、PR、ticket —— 而不是从 diff 开始。

## 它在生效的标志

- 每个已解决的 hunk 都保留了双方的行为，或者在无法保留的地方明确说清了取舍。
- 没有出现任何两边分支上都不存在的新行为。
- 在提交之前，找到并跑通了项目自己的检查 —— 类型检查、测试、格式化。
- merge 或 rebase 被一路推进到一个完成的 commit，绝不中途放弃。

## 它在流程中的位置

这是一个随时可以拿起来用的独立 skill：在 merge 或 rebase 卡住的那一刻调用它，它会把一个干净、已提交的工作树交还给你。它的天然邻居是 [diagnosing-bugs](https://aihero.dev/skills-diagnosing-bugs)，因为一个冲突解决得很干净、但之后行为异常的 merge，是诊断问题，而不是冲突问题。当你不确定哪个 skill 合适时，[ask-matt](https://aihero.dev/skills-ask-matt) 会为你指路。
