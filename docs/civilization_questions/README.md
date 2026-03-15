# Civilization Questions（文明议题）

本目录记录 OpenDatong 项目的 **文明议题** 讨论与结论，采用类似互联网 RFC 的格式。

## 流程

```
Idea → GitHub Issue → Community Discussion → Proposal → Branch → Merge
```

## 已记录议题

| RFC | 标题 | 状态 |
|-----|------|------|
| [0001](question_001_world_nature.md) | Nature of the Digital World | 已采纳：双层模型 |
| — | 重要决定：Ontology v0.1 价值系统 | [Issue #2](https://github.com/menglingqing/opendatong/issues/2) 讨论中 |

## 文明决策（已采纳）

见 [docs/civilization_decisions/](../civilization_decisions/)：Decision 0001 双层世界模型。

---

## 将「重要决定」添加到 GitHub（Issue #2）

在项目根目录执行：

```bash
gh auth login   # 若未登录，先完成认证
gh issue create --title "重要决定：Ontology v0.1 价值系统（儒家 vs 普适文明价值）" --body-file docs/civilization_questions/issue_002_values_body.md
```

创建成功后，可将返回的 Issue 链接补充到 `ontology/README.md` 或本目录说明中。

---

## 创建 Issue #1（若尚未创建）

```bash
gh issue create --title "Civilization Question #1: Dream World vs Structured System" --body-file docs/civilization_questions/issue_001_body.md
```
