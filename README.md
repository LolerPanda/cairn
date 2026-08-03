# 石堆 · Cairn · Draft v0.1

**[中文](#石堆--中文版)** · **[English](#cairn--english)**

---

## 石堆 · 中文版

**石堆(Cairn)** 是一个**模式级架构框架**,面向多智能体、多会话研究/工程工作流的「浮筏时代」——即那种还没稳定下来、状态临时依赖对话历史和人的记忆的初期形态。它描述了浮筏时代的套件是什么、会怎么坏、需要什么样的纪律才能撑住、其交接和检查面应该是什么形状——**这样,读者可以按照这些模式,重建属于自己的套件**。

这份框架**不发布任何套件**。它发布的是:一份套件必须回答的问题清单、一份状态描述必须遵循的词汇表、一份交接必须符合的骨架。名字、角色、套件数量、业务领域、工具选择、具体脚本——都留给读者自己填。

### 这是什么

- 一个**框架**——模式、协议、词汇、纪律
- 一个**检查清单**——套件要在会话死亡后活下来必须回答的问题
- 一个**失败模式目录**——十二个类别,每一个都带模式级别的根因和修复方向
- 一个**方法库**——三种可复用的方法(失败模式普查、原语对比、限定范围复审)

### 这不是什么

- 不是一个套件。这里没有应用。
- 不是一份可执行工具集。这里没有脚本。
- 不是一套工具。没有 `check` 二进制、没有生成器、没有状态文件。
- 不对你的命名、角色或工具链发表意见。仓库里所有 `<system-name>` `<role>` `<suite>` 都是占位符,由你填。
- 不是承诺。模式是模式级的——它们压缩了经验,但是否契合你的项目,由你判断。

### 你能拿到什么 · 你需要自己做什么

**你拿到**:词汇、失败模式目录、协议骨架、方法学、纪律规则——足够让你知道**自己的套件该长什么样才能活下来**。

**你做**:挑名字、挑角色、挑工具、写自己的脚本、接自己的日志格式、决定自己的治理。这份框架告诉你这些工件必须**做什么**,而不是它们该**叫什么**、**怎么实现**。

### 「浮筏时代」套件的一句定义

> 「浮筏时代」的套件是这样的:工作状态活在对话历史和人的记忆里,跨会话的连续性依赖于「有人还在这个房间里」。一旦会话结束,浮筏就散开了。

这份框架是**浮筏时代出过什么问题**的目录,也是**下一次迭代必须长成什么形状**才能活下来的目录。它到这里为止,不规定下一次迭代该长什么样。

### 阅读顺序

新读者:

1. `docs/01-what-is-a-raft-suite.md` — 定义 + 症状清单
2. `docs/02-signs-you-need-this.md` — 自诊断清单
3. `docs/03-glossary.md` — 九个状态词 + 六个一票否决对 + 四个证据等级
4. `docs/04-failure-modes.md` — 十二个失败类别,模式级

准备设计:

5. `docs/05-record-discipline.md` — 七条立即可强制的规则
6. `docs/06-anti-patterns.md` — 六种不该建的形状
7. `docs/07-protocol-skeletons.md` — 五种骨架(交接、冷启动、Owner 队列、角色 playbook、限定范围复审)
8. `docs/08-methodology.md` — 三种可复用方法

准备实施:

9. `docs/09-implementation-checklist.md` — 你的实现必须回答的问题清单
10. `UPGRADE-PATH.md` — 走出浮筏时代的方向,用问题写,不给答案

`templates/` 里的模板是可直接抄的骨架。填 `<占位符>` 就能用。

### Non-goals

- 共识算法(与 Raft 共识算法无关)
- 多智能体编排平台
- LLM 提示工程
- 任何具体论文、项目或组织

### 许可与状态

Draft v0.1。License:**MIT**。首次公开发布,后续持续迭代。

### 版本迭代

这份框架会持续迭代。迭代规则见 `UPGRADE-PATH.md`。新内容尽量追加式落地;规则被撤销时,保留在文件里,加删除线 + 日期备注,让 fork 读者能追踪变更。

### Origin

从多个独立工作流中反复出现的连续性和溯源模式蒸馏而来。项目特定的细节已被移除。

### 为什么叫「石堆」

在荒野里,石堆(cairn)是留给下一个走这条路的人的方向标——不是路本身、不是目的地、不是地图,只是一个「这里有人走过,方向大约是这边」的标记。这份框架的定位与它一样:不告诉你套件该叫什么、长什么样、用什么工具;只告诉你,在「浮筏时代」这段荒野里,前面的人在哪几个坑摔倒过、又是怎么爬出来的。

---

## Cairn · English

**Cairn** is a **pattern-level architecture** framework for suites in their **raft-era** — the pre-fixed state of multi-agent, multi-session research/engineering workflows. It describes what a raft-era suite is, what fails in it, what discipline holds it together long enough to survive, and what shape its handoffs and check surfaces must have — **so a reader can reconstruct their own suite from these patterns**.

This framework **does not ship a suite**. It ships the questions a suite must answer, the vocabulary its state descriptions must use, and the skeletons its handoffs must fit. Names, roles, count of suites, business domain, tool choices, and concrete scripts are all left to the reader.

### What this is

- A **framework** — patterns, protocols, vocabularies, discipline
- A **checklist** — questions a suite must answer to survive session death
- A **failure-mode catalog** — twelve classes with pattern-level root cause and fix direction
- A **methodology library** — three reusable methods (failure-mode census, primitive comparison, scoped reconsideration)

### What this is NOT

- Not a suite. There is no application here.
- Not a runnable kit. There are no scripts.
- Not a set of tools. No `check` binary, no generator, no state file.
- Not opinionated about your names, roles, or tooling. Every occurrence of `<system-name>`, `<role>`, `<suite>` in this repo is a placeholder for you to fill.
- Not a promise. Patterns are pattern-level; they compress hard-won experience but their fit to your project is your judgment.

### What you get, and what you have to do

**You get**: vocabulary, failure-mode catalog, protocol skeletons, methodology, discipline rules — enough to know **what shape your own suite must take** to survive.

**You do**: pick names, pick roles, pick tooling, write your own scripts, wire your own log format, decide your own governance. This framework tells you what those artifacts must *do*; not what they must *be called* or *how they must be implemented*.

### The one-sentence definition of a "raft-era" suite

> A raft-era suite is one where working state lives in conversation history and human memory, and cross-session continuity depends on someone still being in the room. When a session ends, the raft floats apart.

This framework is a catalog of **what went wrong in raft-era**, and **what shape the next iteration must have** to survive. It stops there. It does not prescribe the next iteration itself.

### Reading order

Newcomer:

1. `docs/01-what-is-a-raft-suite.md` — definition + symptom list
2. `docs/02-signs-you-need-this.md` — self-diagnosis checklist
3. `docs/03-glossary.md` — nine status words + six one-vote-vetoes + four evidence tiers
4. `docs/04-failure-modes.md` — twelve failure classes, pattern-level

Practitioner ready to design:

5. `docs/05-record-discipline.md` — seven immediately-enforceable rules
6. `docs/06-anti-patterns.md` — six shapes not to build
7. `docs/07-protocol-skeletons.md` — five skeleton shapes (handoff, cold-start, owner queue, role playbook, scoped reconsideration)
8. `docs/08-methodology.md` — three reusable methods

Practitioner about to implement:

9. `docs/09-implementation-checklist.md` — a checklist of questions your implementation must answer
10. `UPGRADE-PATH.md` — direction of travel past raft-era, in questions not answers

Templates in `templates/` are drop-in skeletons. Fill in `<placeholders>`.

### Non-goals

- Consensus algorithms (this is not related to Raft-the-consensus-algorithm)
- Multi-agent orchestration platforms
- LLM prompt engineering
- Any specific paper, project, or organization

### License and status

Draft v0.1. License: **MIT**. First public release; will iterate.

### Versioning

This framework will iterate. Rules for iteration are in `UPGRADE-PATH.md`. New material lands additive whenever possible; when a rule is retracted, it stays in the file with a strike-through and dated note so anyone reading a fork can trace the change.

### Origin

Distilled from recurring continuity and provenance patterns observed across independent workflows. Project-specific details have been removed.

### Why "Cairn"?

In wilderness, a cairn is a marker left by the person who walked this path first — not the path itself, not the destination, not a map, just a signal that "someone was here, and the way is roughly this direction". The framework carries the same role: it does not tell you what your suite must be called, look like, or use as tools; it tells you where earlier travelers in the raft-era stumbled, and how they climbed out.

---

**Repository structure**

```
cairn/
├── README.md                             # this file (bilingual)
├── LICENSE                               # MIT
├── CONTRIBUTING.md                       # how to iterate (WIP)
├── VERSION                               # v0.1-draft
├── UPGRADE-PATH.md                       # what comes after raft-era (WIP · questions only)
├── docs/
│   ├── 01-what-is-a-raft-suite.md        # definition + symptoms  (STUB)
│   ├── 02-signs-you-need-this.md         # self-diagnosis  (STUB)
│   ├── 03-glossary.md                    # vocabulary  ✓
│   ├── 04-failure-modes.md               # twelve classes  ✓
│   ├── 05-record-discipline.md           # seven rules  (STUB)
│   ├── 06-anti-patterns.md               # six shapes  (STUB)
│   ├── 07-protocol-skeletons.md          # five skeletons  ✓
│   ├── 08-methodology.md                 # three methods  (STUB)
│   └── 09-implementation-checklist.md    # checklist  (STUB)
├── templates/
│   ├── handoff-frontmatter.md            # 5-line frontmatter  (STUB)
│   ├── current-md-shape.md               # cold-read surface  (STUB)
│   ├── owner-queue-row.md                # queue row format  (STUB)
│   ├── role-playbook.md                  # playbook skeleton  (STUB)
│   ├── failure-mode-census.md            # census methodology template  (STUB)
│   └── scoped-reconsideration-request.md # scoped reconsideration handoff  (STUB)
└── examples/
    └── (intentionally empty — see docs/09)
```

`✓` = fully drafted in this pass. `(STUB)` = title + one-line placeholder, awaiting further passes.
