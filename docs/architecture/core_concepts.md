# Core Concepts — The Constitution of the Digital World

**Status:** Draft  
**Discussion:** Open

Before writing code, we define the **primitive concepts** of the world. Just as the physical world has matter, force, and energy, the digital society needs a minimal set of **social primitives**.

---

## 1. World（世界）

The top-level object. The **runtime environment**.

```
World
 ├ agents
 ├ rules
 ├ governance
 ├ resources
 └ history
```

- Runs the social simulation  
- Records history  
- Enforces rules  

---

## 2. Agent（数字公民）

Individuals in the digital world.

```
Agent
 ├ id
 ├ values          # e.g. fairness, cooperation, self_interest
 ├ reputation
 ├ memory
 ├ capabilities
 └ actions
```

Example:

```
Agent_102
  values:
    fairness: 0.8
    cooperation: 0.9
    self_interest: 0.5
```

Agents can: **vote**, **propose**, **cooperate**, **compete**, **mediate**.

**Agent API (minimal abilities):**

- `perceive(world_state)`
- `propose(action)`
- `vote(proposal)`
- `cooperate(agent)`
- `debate(topic)`

---

## 3. Identity（身份）

Every agent has an identity.

```
identity
 ├ creator
 ├ public_key
 ├ join_time
 └ reputation_history
```

May later integrate DID / blockchain identity; for now kept simple.

---

## 4. Reputation（德行 / 声望）

Governance by virtue — high reputation → governance rights.

```
Reputation Score =
  cooperation_score
  + fairness_score
  + trust_score
```

Inspired by **尧舜禅让**: the virtuous are selected to lead. Reputation is the basis for influence and succession.

---

## 5. Governance（治理机制）

Three modes:

| Mode        | Mechanism                    | Description                          |
|------------|------------------------------|--------------------------------------|
| **投票制**  | `vote(proposal)`             | One agent, one vote                  |
| **声望制**  | `influence = reputation`     | Higher reputation → higher weight    |
| **禅让制**  | `leader selects successor`   | Successor must meet reputation threshold |

**Confucian-style succession:** leader selects the best successor by virtue, cooperation, and trustworthiness. The social loop:

```
for each round:
  agents propose actions
  agents vote
  actions executed
  reputation updated
```

Observe: **trust level**, **cooperation rate**, **conflict rate**.

---

## 6. Resource（资源）

Society needs resources for interaction and conflict.

```
resource
 ├ energy
 ├ compute
 ├ tokens
```

Resources drive **competition**, **cooperation**, and **conflict**.

---

## 7. Protocol（协议）

The rules of interaction. Agents communicate and act through **protocols**, not free-form chat.

Examples:

- proposal protocol  
- voting protocol  
- conflict resolution protocol  
- resource allocation protocol  

**Agent Connection Protocol** (how agents join the world):

- `register_agent()`
- `connect_agent()`
- `submit_action()`
- `retrieve_context()`

---

## MVP: First Version

Implement only three mechanisms:

1. **Agent** — identity, values, actions  
2. **Reputation** — cooperation, fairness, trust  
3. **Governance** — propose → vote → execute → update reputation  

Then observe how leaders emerge and how the society behaves.

---

## Context Engine（语境引擎）

Agents need shared:

- **history**
- **knowledge**
- **values**
- **rules**

A **Context Engine** provides this as **collective memory** so that the world has continuity and shared meaning.
