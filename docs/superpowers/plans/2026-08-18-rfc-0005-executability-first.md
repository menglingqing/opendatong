# RFC 0005 · 可执行性优先 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 opendatong 新增 `rfc/0005_executability_first.md`（认知宪法第四条原则）。无其他文件变更。

**Architecture:** 纯文档，1 新增，仅 opendatong 仓库。

**设计依据:** `docs/superpowers/specs/2026-08-18-rfc-0005-executability-first-design.md`（已批准；RFC 全文以 spec §3 定稿为唯一内容来源）

## Global Constraints

- 仓库 git local 身份已配置（menglingqing <1136586419@qq.com>），不要改动
- commit message 按 Task 给出原文，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- RFC 内容逐字来自 spec §3 定稿
- push 前向用户确认；github.com 直连失败时用 `git -c http.proxy=http://127.0.0.1:7897 push origin main`

---

### Task 1: RFC 0005 落盘

**Files:**
- Create: `~/Desktop/opendatong/rfc/0005_executability_first.md`

- [ ] **Step 1: 创建 rfc/0005_executability_first.md**

内容逐字取自 `docs/superpowers/specs/2026-08-18-rfc-0005-executability-first-design.md` 的"## 3. RFC 0005 全文（定稿）"一节（markdown 代码块内，剥离最外层 ````markdown 包裹标记后写入）。要点自查（不替代逐字复制）：六条原则带粗体标题（建议必须可执行 / 可执行性参与方案优先级 / 指令不得越过能力边界 / 批判应推动下一步 / 可执行应可验收 / 最小可执行步优先）；含总约束探索豁免；落地四问为"做什么/谁来做/依赖什么/如何验收"；无"没有替代路径的批判是姿态"字样；原则正文无"每次只改一个变量"（领域实例化中允许出现"只改一个变量"作为领域实践）。若提取内容不符，停止并报 BLOCKED。

- [ ] **Step 2: 验证**

Run: `test -f ~/Desktop/opendatong/rfc/0005_executability_first.md && echo OK`
Expected: `OK`

Run: `grep -c "没有替代路径的批判是姿态\|每次只改一个变量" ~/Desktop/opendatong/rfc/0005_executability_first.md; grep -c "落地四问" ~/Desktop/opendatong/rfc/0005_executability_first.md; grep -c "阴性结果" ~/Desktop/opendatong/rfc/0005_executability_first.md`
Expected: 0；≥2；≥1

Run: `cd ~/Desktop/opendatong && git status --short`
Expected: 仅 rfc/0005_executability_first.md 为新文件

- [ ] **Step 3: 提交**

```bash
cd ~/Desktop/opendatong
git add rfc/0005_executability_first.md
git commit -m "rfc: 0005 认知原则——可执行性优先

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: 验证 + push

**Files:** 无新建

- [ ] **Step 1: 格式检查**

Run: `head -8 ~/Desktop/opendatong/rfc/0005_executability_first.md && tail -4 ~/Desktop/opendatong/rfc/0005_executability_first.md`
Expected: 头部含 Status/Author/Date；尾部为 Open Questions

- [ ] **Step 2: git status 干净**

Run: `cd ~/Desktop/opendatong && git status --short`
Expected: 无未提交文件

- [ ] **Step 3: push（执行前向用户确认）**

```bash
cd ~/Desktop/opendatong && git push origin main
```

---

## Self-Review 记录

- **Spec 覆盖**：§2 一个文件变更 → Task 1；§4 五条验证 → Task 1 Step 2 + Task 2。
- **Placeholder 扫描**：无；RFC 全文以 spec §3 为单一来源。
- **一致性**：grep 负向检查同时覆盖两个阻塞项（"没有替代路径的批判是姿态"=0、"每次只改一个变量"=0，后者注意与领域实例化中合法的"只改一个变量"区分）。
