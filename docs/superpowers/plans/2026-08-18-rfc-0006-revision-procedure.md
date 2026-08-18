# RFC 0006 · 历史结论修正程序 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 opendatong 新增 `rfc/0006_revision_procedure.md`（首部认知治理文书）。无其他文件变更。

**Architecture:** 纯文档，1 新增，仅 opendatong 仓库。

**设计依据:** `docs/superpowers/specs/2026-08-18-rfc-0006-overturning-history-design.md`（已批准；RFC 全文以 spec §3 定稿为唯一内容来源）

## Global Constraints

- 仓库 git local 身份已配置（menglingqing <1136586419@qq.com>），不要改动
- commit message 按 Task 给出原文，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- RFC 内容逐字来自 spec §3 定稿
- push 前向用户确认；github.com 直连失败时用 `git -c http.proxy=http://127.0.0.1:7897 push origin main`

---

### Task 1: RFC 0006 落盘

**Files:**
- Create: `~/Desktop/opendatong/rfc/0006_revision_procedure.md`

- [ ] **Step 1: 创建 rfc/0006_revision_procedure.md**

内容逐字取自 `docs/superpowers/specs/2026-08-18-rfc-0006-overturning-history-design.md` 的"## 3. RFC 0006 全文（定稿）"一节（markdown 代码块内，剥离最外层 ````markdown 包裹标记后写入）。要点自查（不替代逐字复制）：标题为 `RFC-0006: Cognitive Governance — 历史结论修正程序`（不是 Cognitive Principles）；修正程序四条（修正无惩罚 / 修正须显式声明 / 历史须可追溯 / 下游须评估）；操作机制为修正四要素（旧结论/依据/新结论/影响面）；"关系"一节含"吸收关闭"声明。若提取内容不符，停止并报 BLOCKED。

- [ ] **Step 2: 验证**

Run: `test -f ~/Desktop/opendatong/rfc/0006_revision_procedure.md && echo OK`
Expected: `OK`

Run: `grep -c "Cognitive Governance" ~/Desktop/opendatong/rfc/0006_revision_procedure.md; grep -c "新结论" ~/Desktop/opendatong/rfc/0006_revision_procedure.md; grep -c "必要删除除外" ~/Desktop/opendatong/rfc/0006_revision_procedure.md; grep -c "吸收关闭" ~/Desktop/opendatong/rfc/0006_revision_procedure.md`
Expected: ≥2；≥2；1；1

Run: `cd ~/Desktop/opendatong && git status --short`
Expected: 仅 rfc/0006_revision_procedure.md 为新文件（0002、居民卡、core.md 零改动）

- [ ] **Step 3: 提交**

```bash
cd ~/Desktop/opendatong
git add rfc/0006_revision_procedure.md
git commit -m "rfc: 0006 认知治理——历史结论修正程序

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: 验证 + push

**Files:** 无新建

- [ ] **Step 1: 格式与法域检查**

Run: `head -8 ~/Desktop/opendatong/rfc/0006_revision_procedure.md && tail -4 ~/Desktop/opendatong/rfc/0006_revision_procedure.md`
Expected: 头部含 Status/Author/Date 且标题为 Cognitive Governance；尾部为 Open Questions

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
- **一致性**：文件名 0006_revision_procedure.md 与新法域一致；grep 正向检查覆盖三处阻塞项修订（Cognitive Governance、新结论、必要删除除外）与吸收关闭声明。
