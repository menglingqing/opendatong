# Civilization Questions（文明议题）

本目录记录 OpenDatong 项目的 **文明议题** 讨论与结论，采用类似互联网 RFC 的格式。

## 流程

```
Idea → GitHub Issue → Community Discussion → Proposal → Branch → Merge
```

## 已记录议题

| RFC | 标题 | 状态 |
|-----|------|------|
| [0001](question_001_world_nature.md) | Nature of the Digital World | 讨论中 |

## 创建 Issue #1（若尚未创建）

在项目根目录执行：

```bash
gh auth login   # 若未登录，先完成认证
gh issue create --title "Civilization Question #1: Dream World vs Structured System" --body-file docs/civilization_questions/issue_001_body.md
```

创建成功后，将返回的 Issue URL 填入 `question_001_world_nature.md` 中的「讨论」一节。
