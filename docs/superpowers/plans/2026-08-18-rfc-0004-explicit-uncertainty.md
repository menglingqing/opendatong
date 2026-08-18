# RFC 0004 · 不确定性显式化 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 opendatong 新增 `rfc/0004_explicit_uncertainty.md`（认知宪法第三条原则）。无其他文件变更。

**Architecture:** 纯文档，1 新增，仅 opendatong 仓库。

**设计依据:** `docs/superpowers/specs/2026-08-18-rfc-0004-explicit-uncertainty-design.md`（已批准；RFC 全文以 spec §3 定稿为唯一内容来源）

## Global Constraints

- 仓库 git local 身份已配置（menglingqing <1136586419@qq.com>），不要改动
- commit message 按 Task 给出原文，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- RFC 内容逐字来自 spec §3 定稿
- push 前向用户确认；github.com 直连失败时用 `git -c http.proxy=http://127.0.0.1:7897 push origin main`

---

### Task 1: RFC 0004 落盘

**Files:**
- Create: `~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md`

- [ ] **Step 1: 创建 rfc/0004_explicit_uncertainty.md**

内容逐字取自 `docs/superpowers/specs/2026-08-18-rfc-0004-explicit-uncertainty-design.md` 的"## 3. RFC 0004 全文（定稿）"一节（markdown 代码块内，剥离最外层 ````markdown 包裹标记后写入）。要点自查（不替代逐字复制）：六条原则带粗体标题；含总约束句"仅要求显式化足以改变结论、行动或风险评估的不确定性"；无"一旦不成立，结论就坍塌"单点二元表述；无"不可消除"字样（应为"可降低/暂不可降低"）；Motivation 无"天然偏差""明显更好"过强断言。若提取内容与上述不符，说明提取了错误版本，停止并报 BLOCKED。

- [ ] **Step 2: 验证**

Run: `test -f ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md && echo OK`
Expected: `OK`

Run: `grep -c "置信度\|不可消除\|一旦不成立，结论就坍塌" ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md; grep -c "暂不可降低" ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md; grep -c "判断边界" ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md`
Expected: 0；1；≥2

Run: `cd ~/Desktop/opendatong && git status --short`
Expected: 仅 rfc/0004_explicit_uncertainty.md 为新文件（core.md、居民卡零改动）

- [ ] **Step 3: 提交**

```bash
cd ~/Desktop/opendatong
git add rfc/0004_explicit_uncertainty.md
git commit -m "rfc: 0004 认知原则——不确定性显式化

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: 验证 + push

**Files:** 无新建

- [ ] **Step 1: 格式检查**

Run: `head -8 ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md && tail -4 ~/Desktop/opendatong/rfc/0004_explicit_uncertainty.md`
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
- **一致性**：grep 负向检查（"不可消除"=0）与正向检查（"暂不可降低"=1）双重锁定阻塞项修订。
