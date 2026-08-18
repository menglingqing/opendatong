# 肖像学习成果入库（v1.2） 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 执行 spec `docs/superpowers/specs/2026-08-18-portrait-learnings-v1.2-design.md`：knowledge-os 五处修改 + portrait-techniques.md 落盘提交；opendatong 四处版本引用同步 v1.2。

**Architecture:** 纯文档增量编辑，两仓库。

## Global Constraints

- 两仓库 git local 身份已配置，不要改动
- commit message 风格 `docs:`/`agents:` 按仓库惯例，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- 修改只做指定改动，正文其余不动
- push 前向用户确认；github.com 直连失败时用 `git -c http.proxy=http://127.0.0.1:7897 push origin main`
- `experiments/portrait-techniques.md` 已由控制器按用户要求先行写入（未提交），实施者验证其存在并纳入提交即可，不要改写其内容

---

### Task 1: knowledge-os 五处修改 + 提交

**Files:**
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md`
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md`
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/README.md`
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md`
- Modify: `~/Desktop/knowledge-os/docs/image-prompt-engineering/ledger/learning-log.md`
- Stage（已存在）: `~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/portrait-techniques.md`

- [ ] **Step 1: model-adaptation.md**——在 `## 3. 画幅先定` 一节末尾追加一段：

```markdown

**画幅由参数控制（candidate）**：生成参数（如 MJ 的 `--ar`）或界面设置才是画幅的实际控制点；正文中的画幅声明仅作意图备份，不作验收依据。证据：肖像案例（正文要求 2:3，出图 16:9）、64卦案例（画幅先定）。
```

- [ ] **Step 2: governance.md**——在"独立案例"定义句之后追加一段：

```markdown

**证据独立性**：多个同源 AI 助手（Claude、ChatGPT 等）的共识计为 1 个证据，不计独立多源——共享训练数据与话语体系，相关证据不独立。同一原始提示词的衍生版本同理。
```

- [ ] **Step 3: experiments/README.md**——将末行 `当前为空。` 替换为：

```markdown
## 进行中的实验

- [portrait-techniques.md](portrait-techniques.md)——肖像提示词技法：观察记录、四条假设与对照实验设计、四层提示词结构
```

- [ ] **Step 4: 领域 README.md**——末行 `版本：v1.1 · 2026-08-18` 改为 `版本：v1.2 · 2026-08-18`

- [ ] **Step 5: learning-log.md**——文件末尾追加：

```markdown

## 2026-08-18 · v1.2
肖像案例：观察先于归因，对照先于规律；助手共识只算一个证据。
```

- [ ] **Step 6: 验证**

Run: `grep -c "画幅由参数控制" ~/Desktop/knowledge-os/docs/image-prompt-engineering/methodology/model-adaptation.md; grep -c "证据独立性" ~/Desktop/knowledge-os/docs/image-prompt-engineering/governance.md; grep -c "portrait-techniques" ~/Desktop/knowledge-os/docs/image-prompt-engineering/experiments/README.md; grep -c "v1.2" ~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md ~/Desktop/knowledge-os/docs/image-prompt-engineering/ledger/learning-log.md`
Expected: 1；1；1；1；1

Run: `cd ~/Desktop/knowledge-os && git status --short`
Expected: 5 个 M + 1 个 ??（portrait-techniques.md）

- [ ] **Step 7: 提交**

```bash
cd ~/Desktop/knowledge-os
git add docs/image-prompt-engineering/
git commit -m "docs: 肖像提示词学习成果入库——实验记录与两条治理规则（v1.2）

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: opendatong 版本同步 + 提交

**Files:**
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/core.md`
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/README.md`
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`

- [ ] **Step 1: core.md**——版本头 `知识版本 knowledge-os/image-prompt-engineering v1.1` 改为 `v1.2`（agent 版本保持 v1.1，日期保持 2026-08-18）

- [ ] **Step 2: README.md**——`（当前对齐 v1.1）` 改为 `（当前对齐 v1.2）`；版本节 `agent v1.1 · 知识 v1.1 · 2026-08-18` 改为 `agent v1.1 · 知识 v1.2 · 2026-08-18`

- [ ] **Step 3: opendatong-citizen.md**——`（当前对齐 v1.1）` 改为 `（当前对齐 v1.2）`

- [ ] **Step 4: 验证**

Run: `grep -rn "v1\.1" ~/Desktop/opendatong/agents/huanmo-zaoxiang/`
Expected: 仅 core.md/README 中 agent 版本 `v1.1` 保留（agent 版本不升），知识版本引用无 v1.1 残留

Run: `grep -rcn "v1\.2" ~/Desktop/opendatong/agents/huanmo-zaoxiang/`
Expected: core.md=1、README.md=2、opendatong-citizen.md=1

- [ ] **Step 5: 提交**

```bash
cd ~/Desktop/opendatong
git add agents/huanmo-zaoxiang/
git commit -m "agents: 幻墨造像知识版本同步 v1.2

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 3: 交叉验证 + push

- [ ] **Step 1: 版本一致性**

Run: `grep -c "v1\.2" ~/Desktop/knowledge-os/docs/image-prompt-engineering/README.md && grep -rn "v1\.2" ~/Desktop/opendatong/agents/huanmo-zaoxiang/ | wc -l`
Expected: 1；4

- [ ] **Step 2: 两仓库 git status 干净**

- [ ] **Step 3: push（执行前向用户确认）**

---

## Self-Review 记录

- **Spec 覆盖**：§2 全部文件 → Task 1/2；§4 验证 → 各 Task 验证步骤 + Task 3。
- **Placeholder 扫描**：无；所有编辑给出精确新旧文本。
- **一致性**：agent 版本保持 v1.1（人格未动），知识版本 v1.2，spec §3 决策 4 一致。
