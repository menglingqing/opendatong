# RFC 0003 · 证据优先 实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 opendatong 新增 `rfc/0003_evidence_first.md`（认知宪法第二条原则），并将幻墨造像居民身份卡的认知原则行泛化为"RFC 0002 起的认知原则序列"。

**Architecture:** 纯文档，1 新增 + 1 修改，仅 opendatong 仓库。

**设计依据:** `docs/superpowers/specs/2026-08-18-rfc-0003-evidence-first-design.md`（已批准，含两处阻塞项修订与三处措辞修订——以 spec §3 定稿为唯一内容来源）

## Global Constraints

- 仓库 git local 身份已配置（menglingqing <1136586419@qq.com>），不要改动
- commit message 按各 Task 给出原文，附 `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`
- RFC 内容逐字来自 spec §3 定稿（本计划 Task 1 内嵌全文）；居民卡只改一行
- push 前向用户确认；github.com 直连失败时用 `git -c http.proxy=http://127.0.0.1:7897 push origin main`

---

### Task 1: RFC 0003 + 居民卡泛化

**Files:**
- Create: `~/Desktop/opendatong/rfc/0003_evidence_first.md`
- Modify: `~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md`（改 1 行）

- [ ] **Step 1: 创建 rfc/0003_evidence_first.md**

内容逐字取自 spec §3 定稿（`docs/superpowers/specs/2026-08-18-rfc-0003-evidence-first-design.md` 中"## 3. RFC 0003 全文（定稿）"一节内的 markdown 块，剥离外层包裹标记后写入）。要点自查（不替代逐字复制）：六条原则带粗体标题（依据可追溯 / 表达强度受证据约束 / 未知不得伪装为已知 / 不选择性使用证据 / 证据与问题匹配 / 证据无永久效力）；无"一手实测 > 可溯源文档"固定排序句；无"置信度"字样；Motivation 用"普遍/多表现为"而非"全部"。

- [ ] **Step 2: 居民卡改一行**

将 `agents/huanmo-zaoxiang/adapters/opendatong-citizen.md` 中的：

```markdown
- **认知原则**：继承 OpenDatong 认知宪法（[RFC 0002](../../../rfc/0002_cognitive_principles.md)）——顺势完成，逆向校验
```

改为：

```markdown
- **认知原则**：继承 OpenDatong 认知宪法（[RFC 0002](../../../rfc/0002_cognitive_principles.md) 起的认知原则序列）——顺势完成，逆向校验；证据优先
```

- [ ] **Step 3: 验证**

Run: `test -f ~/Desktop/opendatong/rfc/0003_evidence_first.md && echo OK`
Expected: `OK`

Run: `grep -c "置信度" ~/Desktop/opendatong/rfc/0003_evidence_first.md; grep -c "证据与问题匹配" ~/Desktop/opendatong/rfc/0003_evidence_first.md; grep -c "事实性断言" ~/Desktop/opendatong/rfc/0003_evidence_first.md`
Expected: 0；1；1（两处阻塞项修订与断言改名已落入正文）

Run: `cd ~/Desktop/opendatong && git diff --stat agents/`
Expected: opendatong-citizen.md `1 insertion(+), 1 deletion(-)`

- [ ] **Step 4: 提交**

```bash
cd ~/Desktop/opendatong
git add rfc/0003_evidence_first.md agents/huanmo-zaoxiang/adapters/opendatong-citizen.md
git commit -m "rfc: 0003 认知原则——证据优先

Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>"
```

---

### Task 2: 验证 + push

**Files:** 无新建

- [ ] **Step 1: 链接与格式检查**

Run: `head -8 ~/Desktop/opendatong/rfc/0003_evidence_first.md && grep -q "认知原则序列" ~/Desktop/opendatong/agents/huanmo-zaoxiang/adapters/opendatong-citizen.md && echo OK`
Expected: 头部含 Status/Author/Date；输出 `OK`

- [ ] **Step 2: git status 干净**

Run: `cd ~/Desktop/opendatong && git status --short`
Expected: 无未提交文件

- [ ] **Step 3: push（执行前向用户确认）**

```bash
cd ~/Desktop/opendatong && git push origin main
```

---

## Self-Review 记录

- **Spec 覆盖**：§2 两个文件变更 → Task 1；§4 五条验证 → Task 1 Step 3 + Task 2；两处阻塞项修订以 grep 负向/正向双重验证（"置信度"=0、"证据与问题匹配"=1）。
- **Placeholder 扫描**：无；RFC 全文以 spec §3 为单一来源，避免计划与 spec 双写漂移（上次 RFC 0002 的终审证明该路径可靠——Task 1 Step 1 明确要求从 spec 提取）。
- **一致性**：居民卡泛化行与 spec §2 逐字一致。
