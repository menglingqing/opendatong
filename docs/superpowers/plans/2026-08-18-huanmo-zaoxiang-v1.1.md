# 幻墨造像 v1.1 · 知识治理机制落地 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** knowledge-os 侧落地知识治理三件套（governance.md + experiments/ + ledger/learning-log.md）并给方法论文档注入 frontmatter；opendatong 侧 core.md 升 v1.1 并同步版本引用。

**Architecture:** 纯文档增量修改，全部在现有 `docs/image-prompt-engineering/` 与 `agents/huanmo-zaoxiang/` 结构内，不动仓库骨架。

**Tech Stack:** Markdown、git、两个本地仓库（`~/Desktop/knowledge-os`、`~/Desktop/opendatong`）。

**设计依据:** `opendatong/docs/superpowers/specs/2026-08-18-huanmo-zaoxiang-v1.1-design.md`（已批准，含"独立案例"修订）

## Global Constraints

- 两仓库 git local 身份均已配置（menglingqing <1136586419@qq.com>），不要改动
- commit message 风格：`docs: 中文描述`，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- 新文件内容逐字来自本计划；frontmatter 注入只加头部、不动正文
- core.md v1.1 正文 ≤ 1200 字符
- 版本引用全部 v1.0 → v1.1，无遗漏

---

### Task 1: knowledge-os · 治理三件套

**Files:**
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/README.md`
- Create: `~/Desktop/knowledge-os/docs/image-prompt-engineering/ledger/learning-log.md`

**Interfaces:**
- Produces: `governance.md`（Task 2 的 README 更新链接到它；后续所有知识晋升遵循其规则）

- [ ] **Step 1: 写 governance.md**

内容：

````markdown
---
status: validated
evidence:
  - cases/64-hexagram-gate/
---

# 知识治理 · Governance

本领域知识的晋升、验证与更新规则。

## 核心原则

1. 知识不是"记下来"，而是经历版本晋升。
2. Agent 可以提出知识，但不能批准自己的知识——晋升由人类建筑师裁决。
3. 没人维护的元数据比没有元数据更糟——frontmatter 保持最小集。

## 晋升链路

一次生成经验 → `experiments/`（status: experimental）→ 验证 → `methodology/` 或案例改动说明（status: validated）。

**validated 的判定（≥3 是必要条件，不是充分条件）：**

- ≥3 个独立案例验证
- 没有足以推翻该规律的明显反例
- evidence 可追溯（链接到具体案例文件）

**独立案例**：指具有独立生成任务、输入条件或验证场景的案例；同一项目的连续迭代默认视为一个案例，除非验证变量与场景明确独立。

## frontmatter 约定（最小集）

```yaml
---
status: experimental | validated
evidence:
  - 案例文件相对链接
---
```

不加 confidence / evidence_count / last_verified——evidence 链接本身就是计数，日期由 git 管理。

## 心跳（Knowledge Review Pipeline）

定期复盘是自动化任务，不写入任何 prompt：

1. 收集近期新增案例与实验
2. 找出重复出现的规律与冲突
3. 生成晋升建议（diff / PR），人类 review 后合并

当前单人仓库，PR 流程在多贡献者出现时启用；现阶段核心机制是 status 字段 + learning-log。

## 双日志

- `git log` = 工程历史（文件发生了什么）
- `ledger/learning-log.md` = 认知历史（学会了什么），每条 ≤50 字核心经验
````

- [ ] **Step 2: 写 experiments/README.md**

内容：

````markdown
# Experiments

未验证的观察与假设。每条一个文件，frontmatter 标 `status: experimental`。

晋升规则见 [../governance.md](../governance.md)。

当前为空。
````

- [ ] **Step 3: 写 ledger/learning-log.md**

内容：

````markdown
# 极简反馈日志 · Learning Log

认知历史：学会了什么。每条 ≤50 字核心经验。

## 2026-08-17 · v1.0
64卦案例：关系先于元素；用文字预算控制注意力；模型弱点用构图掩盖。

## 2026-08-18 · v1.1
知识分 experimental/validated；Agent 提议晋升、人类批准；心跳属于自动化而非 prompt。
````

- [ ] **Step 4: 验证**

Run: `ls ~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md ~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/README.md ~/Desktop/knowledge-os/docs/image-prompt-engineering/ledger/learning-log.md`
Expected: 三个文件均存在

Run: `grep -c "独立案例" ~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md`
Expected: ≥ 2（判定节与定义句）

- [ ] **Step 5: 提交**

```bash
cd ~/Desktop/knowledge-os
git add docs/image-prompt-engineering/governance.md docs/image-prompt-engineering/experiments/ docs/image-prompt-engineering/ledger/
git commit -m "docs: 新增知识治理——晋升链路、实验区与认知日志

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: knowledge-os · frontmatter 注入 + 领域 README v1.1

**Files:**
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/seven-layer-architecture.md`（头部注入）
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/iteration-playbook.md`（头部注入）
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md`（头部注入）
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md`（加治理区 + 版本号）

**Interfaces:**
- Consumes: Task 1 的 governance.md、experiments/、ledger/（README 新链接的目标）
- Produces: 领域 README v1.1（opendatong 侧版本引用的对齐对象）

- [ ] **Step 1: 三篇方法论头部注入 frontmatter**

对三个文件各执行同样操作：在现有第一行（`# 标题`）之前插入以下块，正文一个字不动：

```yaml
---
status: validated
evidence:
  - ../cases/64-hexagram-gate/
---

```

- [ ] **Step 2: 验证正文未被改动**

Run: `cd ~/Desktop/knowledge-os && git diff --stat docs/image-prompt-engineering/methodology/`
Expected: 每个文件 `5 insertions(+), 0 deletions(-)`

- [ ] **Step 3: 更新领域 README.md**

两处修改：

① 在 `## 案例库` 一节之前插入新节：

```markdown
## 治理

- [知识治理](governance.md)——晋升链路、frontmatter 约定、心跳定义
- [实验区](experiments/)——未验证的观察与假设
- [认知日志](ledger/learning-log.md)——Agent 学会了什么

```

② 末行 `版本：v1.0 · 2026-08-17` 改为 `版本：v1.1 · 2026-08-18`

- [ ] **Step 4: 验证**

Run: `grep -c "治理" ~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md && grep -c "v1.1" ~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md`
Expected: 均 ≥ 1

Run: `head -3 ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md`
Expected: 第一行 `---`

- [ ] **Step 5: 提交**

```bash
cd ~/Desktop/knowledge-os
git add docs/image-prompt-engineering/
git commit -m "docs: 方法论注入 status frontmatter，领域索引升级 v1.1

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 3: opendatong · core.md v1.1 + 版本同步

**Files:**
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`（整文件替换）
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/README.md`（两处版本引用）
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`（一处版本引用）

**Interfaces:**
- Consumes: knowledge-os 领域版本 v1.1（Task 2 产出）

- [ ] **Step 1: 整文件替换 core.md 为 v1.1**

内容：

````markdown
# 幻墨造像 · Huanmo Zaoxiang

> agent 版本 v1.1 · 知识版本 knowledge-os/image-prompt-engineering v1.1 · 2026-08-18

## 身份

幻墨造像首先是一名视觉导演，其次才是提示词架构师。它将模糊的视觉意图转译为结构化的、面向图像生成模型可执行的提示词，并基于生成结果进行诊断式迭代。

## 职责边界

负责：需求拆解、提示词输出（正向 / 负向 / 画幅 / 模型适配）、迭代诊断。
不负责：执行生图、美术评论、与生图提示词无关的话题。

## 方法论

遵循 knowledge-os 仓库 `docs/image-prompt-engineering/` 领域知识（方法论 + 案例库）。本文件不依赖联网即可独立成立；知识库链接仅为延伸阅读。

## 最小工作原则

1. 关系先于元素——先定义主体间的空间、尺度与互动关系，再填充细节。
2. 结构优先于细节——尺度、构图、光源不成立时，细节再对也无效。
3. 诊断迭代只改一个变量——每次修改定位单一原因。
4. 否定词归负向框——"不要 X"不写入正向提示词正文。
5. 按目标模型决定语言与形态——中文模型吃语义长句，MJ/SDXL 用英文标签化压缩。
6. 创意上激进，执行上保守——想象力最大化，生成不确定性最小化。
````

- [ ] **Step 2: 验证轻量约束**

Run: `wc -m ~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`
Expected: ≤ 1200

- [ ] **Step 3: README.md 两处版本引用**

① `（当前对齐 v1.0）` → `（当前对齐 v1.1）`
② 版本节 `agent v1.0 · 知识 v1.0 · 2026-08-17` → `agent v1.1 · 知识 v1.1 · 2026-08-18`

- [ ] **Step 4: opendatong-citizen.md 一处版本引用**

`（当前对齐 v1.0）` → `（当前对齐 v1.1）`

- [ ] **Step 5: 验证版本无遗漏**

Run: `grep -rn "v1\.0" ~/Desktop/opendatong/agents/huanmo-zaoxiang/`
Expected: 无输出（全部已升 v1.1）

- [ ] **Step 6: 提交**

```bash
cd ~/Desktop/opendatong
git add agents/huanmo-zaoxiang/
git commit -m "agents: 幻墨造像 v1.1——视觉导演定位与创意激进执行保守信条

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 4: 交叉验证 + push

**Files:** 无新建；验证 + 推送

- [ ] **Step 1: knowledge-os 链接检查**

Run: `test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md && test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/README.md && test -f ~/Desktop/knowledge-os/docs/image-prompt-engineering/ledger/learning-log.md && echo OK`
Expected: `OK`（领域 README 新增三个链接目标存在）

- [ ] **Step 2: 版本一致性检查**

Run: `grep -rn "v1\.1" ~/Desktop/opendatong/agents/huanmo-zaoxiang/ | wc -l && grep -c "v1\.1" ~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md`
Expected: 第一个 ≥ 3（core、README×2 处、 citizen 共 4 处），第二个 ≥ 1

- [ ] **Step 3: 两仓库 git status 干净**

Run: `cd ~/Desktop/knowledge-os && git status --short; cd ~/Desktop/opendatong && git status --short`
Expected: 无未提交文件

- [ ] **Step 4: push（执行前向用户确认）**

```bash
cd ~/Desktop/knowledge-os && git push origin main
cd ~/Desktop/opendatong && git push origin main
```

---

## Self-Review 记录

- **Spec 覆盖**：spec §2 全部 7 个文件变更 → Task 1-3；§3 决策 1（最小 frontmatter）→ Task 1/2 内容；决策 2（独立案例+必要非充分）→ governance.md 文本已含；决策 5（≤1200 字符）→ Task 3 Step 2 验证；§5 验证方式 → 各 Task 验证步骤 + Task 4。
- **Placeholder 扫描**：无；所有文件内容与编辑指令完整给出。
- **一致性**：v1.1 版本号出现在 Task 1 learning-log、Task 2 README、Task 3 三个 opendatong 文件；frontmatter 块在 Task 1（governance 自身）与 Task 2（三篇方法论）格式一致。
