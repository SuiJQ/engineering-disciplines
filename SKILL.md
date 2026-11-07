---
name: dev-disciplines
description: 通用工程纪律与方法论速查，独立于任何具体项目。当接到全仓审计、排查"零件没接线"类缺陷、写验证判据、管理决策台账、做大文件结构性改动、处理幂等/续跑/中文匹配失效、设计截断压缩或给存量系统加新字段等任务时，按情形查索引定位对应的施工法（procedure）或经验规则（wiki），并按条目的 Steps 执行。用于代码审查、缺陷定位、判据设计、可维护性决策等各类工程维护工作。
---

# Dev Disciplines — 工程纪律与方法论速查

从长期工程实践中提炼的可跨项目复用方法论。按「当前情形」检索，不按目录浏览。

## 用法

1. 对照下方**情形索引**找到最贴近的一到几条。
2. 打开对应 `references/` 条目：`procedure/`（带 Steps 的施工法）或 `wiki/`（经验规则）。
3. 施工法按 Steps 执行；经验规则直接采纳其判据。每条末尾的 Failure modes / Sources 说明失效边界与出处。

## 情形索引

**全仓审计 · 查漏**
- 排查「零件齐全但没接线 / 写了从没被接上」→ `references/procedure/unwired-parts-audit-runbook.md`
- 审计一个成熟模块，想知道哪里最可能有价值 → `references/wiki/audit-effort-goes-to-checking-promises.md`（核对承诺，不在读代码）
- 端到端验证需分离开发者/用户/模型/产物视角 → `references/procedure/four-perspective-ab-axis-verification.md`

**写验证判据 · 让判据可信**
- 一条规则只写在文档里、靠人自觉 → `references/procedure/invariants-as-executable-assertions.md`（写成会红的断言）
- 判据全绿但不可信，分不清写错/没跑/漏扫 → `references/wiki/criteria-credibility-three-failure-modes.md`
- 判据只断言结果形状、不追问结果从哪来 → `references/wiki/criteria-check-provenance-not-shape.md`
- 判据要能证伪、断言可观测行为差异 → `references/wiki/criteria-must-assert-behavior-differences.md`
- 参数在装配链中途被丢弃、既有测试却全绿 → `references/procedure/wiring-defects-need-assembly-root-observation.md`
- 做证伪实验、还原后重跑全量 → `references/procedure/falsification-backup-taken-before-edit.md`

**决策 · 台账**
- 决策只存在于对话/注释里、引用查不到编号 → `references/procedure/land-decisions-to-single-authority.md`
- 自称"事实源"的文档/台账可能说谎 → `references/wiki/docs-and-ledgers-are-not-source-of-truth.md`

**大文件改动 · 事故恢复**
- 结构性搬移 / 正则批量改写大文件 → `references/procedure/large-file-edit-recovery-discipline.md`

**自动修复 · 门禁**
- 自动修复 / 门禁检查途中改被检查对象 → `references/procedure/auto-fix-must-be-visible.md`
- 输出停在「写正文。」「现在写出。」等宣告、零文件产出 → `references/procedure/bind-commitment-to-artifact.md`

**缺陷识别**
- 现象与历史记录完全一致 → `references/wiki/historical-defect-precise-reproduction-identification.md`（判为历史缺陷复现）
- 幂等/断点续跑：记账 id 与判定 id 各拼各的 → `references/wiki/idempotency-identity-and-skip-readback.md`
- 涉及中文的匹配逻辑只测了 ASCII → `references/wiki/cjk-blind-tests-falsely-green.md`（必然假绿）
- 给存量系统新增状态字段 → `references/wiki/memory-gate-zero-destructive-intro.md`（零破坏引入）

**容量 · 上下文**
- 截断 / 压缩上限该留多少 → `references/wiki/truncate-by-token-budget-not-count.md`（按 token 预算，不按条数）

**装配 · 能力 · 环境**
- 一个能力要真发生：意图 / 工具名 / 程序接线三层 → `references/wiki/three-layers-intent-tool-name-program-wiring.md`
- 流程在阶段切换被硬约束拦截、状态全空 → `references/procedure/hard-constraint-validation-state-update-fix.md`
- pytest 报 `ModuleNotFoundError: No module named 'tests'` → `references/wiki/pytest-tests-package-import-fix.md`

## 维护约定

- 新增方法论：先判断是带 Steps 的**施工法**还是**经验规则**，分别放入 `references/procedure/` 或 `references/wiki/`，文件名用小写连字符，保留 `name` / `description` / `kind` frontmatter，并在上方索引补一行。
- 条目间避免互相复制正文，用行内链接指向彼此的 Failure modes。
- 本 skill 只收**跨项目通用**的方法论；某个项目独有的裁决、进度、产物路径不要进这里。