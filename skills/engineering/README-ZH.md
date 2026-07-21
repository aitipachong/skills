# Engineering（工程类技能）

我在日常写代码时使用的技能集合。

## 用户触发型（User-invoked）

只能在你手动输入命令时触发（Claude Code：`disable-model-invocation: true`；Codex：在 `agents/openai.yaml` 中设置 `policy.allow_implicit_invocation: false`）。

- **[ask-matt](./ask-matt/SKILL.md)** —— 询问哪种技能或流程适合你的当前情况。它是本仓库中所有用户触发型技能的路由器。
- **[grill-with-docs](./grill-with-docs/SKILL.md)** —— 拷问式会话（grilling session），同时构建你项目的领域模型：打磨术语，并就地更新 `CONTEXT.md` 和 ADR（架构决策记录）。
- **[triage](./triage/SKILL.md)** —— 通过一套由多个分类（triage）角色组成的状态机来推进 issue 的流转。
- **[improve-codebase-architecture](./improve-codebase-architecture/SKILL.md)** —— 扫描代码库，寻找可以"深化"（deepening）的机会，以可视化 HTML 报告的形式呈现出来，然后针对你选中的那一项进行拷问式深挖。
- **[setup-matt-pocock-skills](./setup-matt-pocock-skills/SKILL.md)** —— 为工程类技能配置本仓库（issue 追踪器、triage 标签、领域文档布局）。每个仓库只需运行一次。
- **[to-spec](./to-spec/SKILL.md)** —— 将当前对话转化为一份规格说明（spec），并发布到 issue 追踪器。
- **[to-tickets](./to-tickets/SKILL.md)** —— 把任何计划、规格说明或对话拆解成一组"示踪子弹"（tracer-bullet）式工单，每个工单都声明其阻塞依赖边——可以是本地文件中的纯文本，也可以是真实追踪器上的原生阻塞链接。
- **[implement](./implement/SKILL.md)** —— 按照规格说明或一组工单所描述的内容来构建工作，在预先约定好的接缝处驱动 `/tdd`，并在提交前以 `/code-review` 收尾。
- **[wayfinder](./wayfinder/SKILL.md)** —— 规划一大块工作——大到单个 agent 会话装不下的程度——把它变成 issue 追踪器上一张由决策工单组成的共享地图，一次解决一个，直到通往目的地的路变得清晰。

## 模型触发型（Model-invoked）

模型或用户均可触发（带有丰富的触发措辞，方便模型主动选用）。

- **[prototype](./prototype/SKILL.md)** —— 构建一个用完即弃的原型来回答某个设计问题：要么是一个可运行的终端应用（用于状态/逻辑），要么是多个可切换的 UI 变体。

- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)** —— 针对疑难 bug 和性能回归的规范化诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./research/SKILL.md)** —— 针对某个问题，依据高可信度的一手资料进行调研，并将发现以带引用的 Markdown 文件形式捕获到仓库中，以后台 agent 方式运行。
- **[tdd](./tdd/SKILL.md)** —— 采用红-绿-重构循环的测试驱动开发。一次一个垂直切片地构建功能或修复 bug。
- **[domain-modeling](./domain-modeling/SKILL.md)** —— 主动构建并打磨项目的领域模型——挑战术语、用场景做压力测试、就地更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./codebase-design/SKILL.md)** —— 用于设计"深模块"（deep modules）的共享纪律与词汇表：小接口、干净的接缝、可通过接口测试。
- **[code-review](./code-review/SKILL.md)** —— 对自某个固定点以来的 diff 进行双轴评审：**规范（Standards）**（是否遵循仓库的编码规范，外加 Fowler 异味基线？）和**规格（Spec）**（是否忠实实现了原始 issue/PRD？），以并行子 agent 方式运行。
- **[resolving-merge-conflicts](./resolving-merge-conflicts/SKILL.md)** —— 逐块处理进行中的 git merge 或 rebase 冲突，通过追溯到每一方的一手来源、按意图来解决，然后完成整个操作——绝不使用 `--abort`。
