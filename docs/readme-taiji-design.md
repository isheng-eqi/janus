# Janus README 太极阴阳美学改进设计方案

> 将 Janus 的太极视觉体系映射到 GitHub Markdown 的约束空间。
> 不用 ANSI，不用 emoji。只用 Markdown 原语表达阴阳。

---

## 一、当前 README 的太极问题诊断

### 1.1 整体结构扫描

当前 README（212 行）由 12 个章节 + 12 条 `---` 分隔线组成：

```
# Janus                           ← 标题
<p> subtitle                      ← HTML 副标题
<p> badges                        ← HTML badges
---                               ← 分隔线 1
**hook 段落**                     ← 浓墨核心断言
解释段落                          ← 正文
---                               ← 分隔线 2
## Why Janus Exists               ← 表格对比
---                               ← 分隔线 3
## Architecture                   ← ASCII 大图
---                               ← 分隔线 4
## Quick Start                    ← 代码块
---                               ← 分隔线 5
## Core Mechanisms                 ← 8 个机制列表
---                               ← 分隔线 6
## Design Philosophy              ← 引用块 + 列表
---                               ← 分隔线 7
## Documentation                  ← 文档表
---                               ← 分隔线 8
## How Janus Differs              ← 对比表
---                               ← 分隔线 9
## Contributing                   ← 列表
---                               ← 分隔线 10
## License                        ← 单行
---                               ← 分隔线 11
<p> footer                        ← HTML 尾部
```

### 1.2 违反太极原则的五个核心问题

#### 问题一：阴阳失调——分隔线泛滥（违反"阴阳""黑白"原则）

**现状：** 12 条 `---` 分隔线，每两个语义块之间都用一道"硬刀切"分开。

**太极诊断：** `---` 在 Markdown 中是强视觉元素——它是 `<hr>` 标签，渲染成一条横贯页面的线。这相当于在每两个房间之间砌一堵墙，而不是留走廊。太极的"阴"应该是**空行留白**——无形、无声、无装饰的呼吸空间。12 条分隔线把 README 切成了 12 个"隔间"，读者感觉到的不是节奏，是碎片化。

**严重程度：CRITICAL。**

#### 问题二：装饰喧宾夺主（违反"黑白"原则）

**现状：**
- 第 3-5 行：`<p align="center"><h3 align="center">` 用 HTML 标签包裹副标题
- 第 7-11 行：`<p align="center"><a><img>` 三枚 shields.io 徽章
- 第 210-212 行：`<p align="center"><sub>` HTML 尾部

**太极诊断：** "黑白"原则要求底色为主，装饰只起点缀作用。徽章（badges）是互联网时代的"门钉"——有用但非必要。HTML 居中标签在纯 Markdown 视角下属于侵入式元素，破坏了 Markdown 的质朴感。三枚徽章并列时，视觉重量不亚于一段正文，成了 README 的"第三主角"。

**严重程度：MAJOR。**

#### 问题三：缺少真正的"阴"——没有呼吸段落（违反"阴阳"原则）

**现状：** Architecture 大图（48 行 ASCII art）之后紧接一行粗体总结 → `---` → Quick Start。信息密度极高的区块之间没有"吸收时间"。

**太极诊断：** 阴阳原则要求 "语义块之间必有一行空行"。但仅有空行只是及格线。对于 Architecture 这种"阳中之阳"（48 行的 ASCII 框图，是整个 README 视觉最重的元素），它前后需要的是**加倍的留白**——不是技术上的空行，而是视觉上的"静默区"。读者看到架构图需要 5-10 秒消化，但当前设计在 0.1 秒后就推给他下一段信息。

**严重程度：MAJOR。**

#### 问题四：标题层级单一——缺乏层次变化（违反"动静"原则）

**现状：** 除了 `# Janus` 是一级标题，其余所有章节标题全是 `##`，共 11 个二级标题平铺。

**太极诊断：** "动静"原则要求长内容有层次变化。11 个同级标题意味着 README 的结构深度为 1——像一张平铺的清单，没有主次、没有纵深。读者无法一眼判断"Architecture"和"License"的重要性差异。对于 Janus 而言，Architecture 和 Design Philosophy 应该是"重章节"，Documentation 和 Contributing 应该是"轻章节"，但当前它们在结构上完全等价。

**严重程度：MINOR（改进后效果提升显著）。**

#### 问题五：刚柔未分——语气一致但缺乏收放（违反"刚柔"原则）

**现状：** 全文语气统一——自信、直接、对比鲜明。这在"Why Janus Exists"和"How Janus Differs"中恰如其分（刚），但在 Design Philosophy 中也延续了同样的硬度。

**太极诊断：** "刚柔"原则要求关键断言用强硬表达（刚），介绍性/反思性内容用温和表达（柔）。Design Philosophy 区块的核心引用（"Agent managing Agent should mirror Human managing Human"）已经用了引用块（柔的容器），但其下方的对比列表没有足够的"收"——它应该比 Why Janus Exists 更温和、更有邀请感，而不是继续"进攻"。

**严重程度：MINOR。**

### 1.3 做得好的地方

在批评之前，先承认当前 README 已经做到的太极正面实践：

| 原则 | 当前实践 | 评价 |
|------|---------|------|
| **无 emoji** | 全文零 emoji | ✅ 完美 |
| **浓墨粗体** | 开篇 "Janus is not another agent framework" 用 `**` | ✅ 炸裂开篇 |
| **引用点睛** | Design Philosophy 和 Quick Start 各有一段 `>` | ✅ 引用块用法正确 |
| **代码块留白** | 代码块前后有空行 | ✅ 基本的阴阳呼吸 |
| **表格克制** | 三张表格都简洁，无多余列 | ✅ 信息密度合理 |

---

## 二、整体结构的阴-阳分段图

以下是改进后的 README 结构，按"阴阳呼吸区"重新组织：

```
┌─────────────────────────────────────────────────────────┐
│                    阳区 1 · 门面                          │
│  # Janus                                                │
│  *Human Management Wisdom → Agent Architecture*         │
│                                                         │
│  **Janus is not another agent framework.** ...          │
│                                                         │
│  （阴·大呼吸 — 3 行空行）                                 │
├─────────────────────────────────────────────────────────┤
│                    阳区 2 · 说服                          │
│  ## Why Janus Exists                                    │
│  [对比表]                                                │
│  Janus's insight 段落                                    │
│                                                         │
│  （阴·小呼吸 — 2 行空行）                                 │
│                                                         │
│  ## Architecture                                        │
│  [ASCII 框图]                                            │
│  **Four roles. Hard boundaries. No overlap.**           │
│                                                         │
│  （阴·大呼吸 — 3 行空行）                                 │
├─────────────────────────────────────────────────────────┤
│                    阳区 3 · 行动                          │
│  ## Quick Start                                         │
│  ```bash ... ```                                        │
│  ```text ... ```                                        │
│  > Requirements: ...                                    │
│                                                         │
│  （阴·中呼吸 — 2 行空行）                                 │
├─────────────────────────────────────────────────────────┤
│                    阳区 4 · 深度                          │
│  ## Core Mechanisms                                     │
│                                                         │
│  **Gatekeeper Tree** — ...                              │
│  **Five-Level Review** — ...                            │
│  **Commander's Intent** — ...                           │
│  （8 个机制，每两个之间空一行）                              │
│                                                         │
│  （阴·中呼吸 — 2 行空行）                                 │
├─────────────────────────────────────────────────────────┤
│                    阳区 5 · 哲学                          │
│  ## Design Philosophy                                   │
│  > "Agent managing Agent should mirror..."              │
│  >                                                     │
│  > This is not a metaphor...                            │
│                                                         │
│  *Every design decision starts with one question...*    │
│  - Military command chains → ...                        │
│  - Judicial review → ...                                │
│                                                         │
│  （阴·小呼吸 — 1 行空行）                                 │
│                                                         │
│  ## How Janus Differs                                   │
│  [对比表]                                                │
│                                                         │
│  （阴·中呼吸 — 2 行空行）                                 │
├─────────────────────────────────────────────────────────┤
│                    阳区 6 · 收口                          │
│  ## Documentation                                       │
│  [文档表]                                                │
│                                                         │
│  ---                                                    │
│                                                         │
│  ## Contributing                                        │
│  1. Fork ...                                            │
│                                                         │
│  ## License                                             │
│  MIT © 2026                                             │
│                                                         │
│  （阴·终 — 纯白，不写任何东西，让读者目光自然落下）          │
└─────────────────────────────────────────────────────────┘
```

### 关键变化

| 维度 | 当前 | 改进后 |
|------|------|--------|
| 分隔线 `---` | 12 条 | **1 条**（仅收口区前） |
| HTML 标签 | 3 处（副标题、徽章、尾部） | **0 处** |
| 呼吸区 | 没有明确的大呼吸 | **3 个大呼吸 + 3 个中呼吸** |
| 标题层级 | 1 个 `#` + 11 个 `##` | 不变（Markdown 约束），但通过呼吸区分主次 |
| 引用块 | 2 处 | **3 处**（增加一处给 Why Janus Exists 的点睛） |

---

## 三、逐段改进建议

### 3.1 阳区 1 · 门面（Title + Hook）

**现状问题：** HTML 标签、徽章、过早出现分隔线。

**改进方案：**

```markdown
# Janus

*Human Management Wisdom → Agent Architecture*

**Janus is not another agent framework. It's a design philosophy that asks: "How do humans manage humans?" — then maps the answer to LLM agents.**

Most frameworks give you tools to build agents. Janus gives you a **management system** for agents — four specialized roles with hard boundaries, inherited from 3,000+ years of human organizational wisdom: military command chains, judicial review standards, manufacturing quality control, academic peer review.
```

**设计理由：**
- 去掉所有 HTML 标签。副标题用 `*斜体*`（淡墨），保持 Markdown 纯粹。
- 去掉 shields.io 徽章——它们的信息（License MIT, Python 3.10+, Status Active）在正文和底部 License 中自然呈现。如果必须保留徽章，放在底部 License 段落旁边作为最小化的一行。
- 门面区块**不用任何分隔线**——开门见山，一气呵成。
- 门面末尾留 **3 行空行**（大呼吸），让读者在进入"说服"之前有一个视觉停顿。

### 3.2 阳区 2 · 说服（Why Janus Exists + Architecture）

**现状问题：** 两个高度相关的章节被 `---` 硬切开。Architecture 图后没有呼吸。

**改进方案：**

```markdown
## Why Janus Exists

Existing agent frameworks are designed around **what LLMs can do**. Janus is designed around **how humans organize**.

| Framework | Core Metaphor | The Problem |
|-----------|--------------|-------------|
| **LangGraph** | State machine / graph | You design the control flow. Great when you know the path. Fails when you don't. |
| **AutoGen** | Conversation / chat | Agents talk. But conversation isn't management — there's no hierarchy, no audit, no accountability. |
| **CrewAI** | Role-playing team | Fun metaphor, but roles have no hard boundaries. Anyone can do anything. |
| **MetaGPT** | Software company SOP | Powerful for code generation. But the SOP is rigid — it's a script, not a management system. |

**Janus's insight:** LLM agents suffer from the same structural problems as human organizations — task decomposition quality varies, outputs deviate from intent, failures cascade silently, and there's no independent audit. Humans solved these problems with **hierarchical management, independent review, graded escalation, and context discipline**. Janus applies those solutions directly.


## Architecture
```

**设计理由：**
- "Why Janus Exists"和"Architecture"放在同一个阳区——它们是"说服"的两面：先讲 why，再 show how。之间只用空行（阴），不用分隔线（刀切）。
- 对比表的第一行加粗关键词（`**what LLMs can do**` vs `**how humans organize**`），浓墨点出核心差异。
- Architecture 图后面留 **3 行空行**（大呼吸），让读者消化完架构图后再进入"行动"区。

### 3.3 阳区 3 · 行动（Quick Start）

**现状问题：** Requirements 注释用了引用块（`>`），但它是实用信息而非哲学声明。

**改进方案：**

```markdown
## Quick Start

```bash
git clone https://github.com/isheng-eqi/janus-agent.git
cd janus
pip install pyyaml colorama openai
echo 'DEEPSEEK_API_KEY=sk-...' > .env
python main.py
```

```text
❯ 帮我写一个 Python 脚本来排序 CSV 文件

Gatekeeper → Planner → Workers → Reviewer → Report

✅ task-1: Parse CSV reading logic — PASSED
✅ task-2: Implement sorting algorithm — PASSED
✅ task-3: Write output with error handling — PASSED

产出文件: ./output/sort_csv.py
```

*Requirements: Python 3.10+, DeepSeek API key. See [config.yaml](config.yaml) for advanced configuration.*
```

**设计理由：**
- Requirements 从引用块改为斜体（淡墨）——它不是哲学声明，而是辅助信息。淡墨恰如其分。
- 示例输出中的 `❯` 是 Unicode 字符，不是 emoji——可以使用。
- Quick Start 后留 **2 行空行**（中呼吸），过渡到深度机制。

### 3.4 阳区 4 · 深度（Core Mechanisms）

**现状问题：** 8 个机制紧挨着列出，视觉上是一堵文字墙。

**改进方案：**

```markdown
## Core Mechanisms

**Gatekeeper Tree** — Tasks decompose recursively. The Gatekeeper decides WHAT, the Planner decides HOW, Workers execute, Reviewer audits. Every layer has a single responsibility with hard boundaries.

**Five-Level Review** — Not just pass/fail. `APPROVED` | `APPROVED_WITH_NOTES` | `MINOR_REVISIONS` | `MAJOR_REVISIONS` | `REJECTED`. Inherited from academic peer review.

**Commander's Intent** — Workers don't just get "what to do." They get `intent` — why this task matters in the bigger picture.

**Immutable Anchor** — The user's original words travel untouched through every layer. No telephone game.

**Self-Healing Recovery** — When tasks fail, the Gatekeeper diagnoses WHY, reformulates strategy, and re-executes.

**Self-Evolution** — Workers record execution experience; the Planner references historical patterns, making the system smarter with every run.

**Intent Validation** — Before delivering results, one final check: "Is this what the user actually asked for?"

**Context Discipline** — Every role sees only what it needs. Inherited from management's "span of control."
```

**设计理由：**
- 重组为 8 个独立段落，每个以 **粗体机制名** 开头（浓墨），后跟淡墨解释。
- 核心机制按重要性排列：Gatekeeper Tree（架构核心）→ Five-Level Review（审查核心）→ Commander's Intent（哲学核心）→ 其余。
- **去掉 Four-Level Defect Severity 作为独立条目**——它是 Five-Level Review 的子概念，合入第二条的自然语言中即可。
- 每两个机制之间空一行（微呼吸），机制组结束后留 **2 行空行**。

### 3.5 阳区 5 · 哲学（Design Philosophy + How Janus Differs）

**现状问题：** 引用块后的列表语气太"刚"，和引用块的"柔"形成冲突。Design Philosophy 和 How Janus Differs 被 `---` 切开。

**改进方案：**

```markdown
## Design Philosophy

> **"Agent managing Agent should mirror Human managing Human."**
>
> This is not a metaphor. It's Janus's first design principle.

*Every design decision starts with one question: "How do human organizations solve this?" — not "What's the most efficient technical solution?"*

- Military command chains → Gatekeeper → Planner → Worker hierarchy
- Judicial review standards → Five-level graded verdicts
- Manufacturing quality control → Three lines of defense, four-level defect severity
- Academic peer review → Independent Reviewer, revision-and-resubmit
- Commander's Intent → `TaskSpec.intent` — know WHY, not just WHAT
- Span of Control → Context discipline — each role sees exactly what it needs

*We have 3,000+ years of organizational wisdom. Janus applies it to LLMs.*
[Read the full philosophy →](docs/design-philosophy.md)


## How Janus Differs

| Aspect | LangGraph / AutoGen / CrewAI | Janus |
|--------|------------------------------|-------|
| **Design principle** | "What can LLMs do?" | "How do humans manage?" |
| **Architecture** | You design the flow | Four-role system with hard boundaries |
| **Task decomposition** | Manual graph / conversation flow | Recursive Gatekeeper Tree with independent audit |
| **Quality control** | Built-in pass/fail at best | Five-level verdict + four-level defect severity |
| **Failure handling** | Retry loop | Diagnosis → strategy reformulation → re-execution |
| **Context management** | Full history or manual pruning | Role-based context discipline |
| **Intent alignment** | Implicit | Explicit: immutable anchor + pre-delivery validation |
```

**设计理由：**
- 引用块保持（好），但下面的列表从 "We have 3,000+ years..."（刚）改为斜体（柔），温和收束。
- "Read the full philosophy →" 用箭头而非括号，更轻。
- Design Philosophy 和 How Janus Differs 之间不用分隔线，只用空行——它们在哲学层面是连续的。

### 3.6 阳区 6 · 收口（Documentation + Contributing + License）

**现状问题：** 三个"轻章节"各自有 `---` 分隔线，过于隆重。

**改进方案：**

```markdown
## Documentation

| Document | Description |
|----------|-------------|
| [**Whitepaper (PDF)**](paper/janus_whitepaper.pdf) | Full technical whitepaper |
| [**Whitepaper (Chinese)**](paper/janus_whitepaper_zh.html) | 中文版白皮书 |
| [**Design Philosophy**](docs/design-philosophy.md) | Why human management patterns |
| [**Human Management Patterns**](docs/human-management-patterns.md) | 6 organizational domains mapped to agents |
| [**config.yaml**](config.yaml) | Configuration reference |

---

## Contributing

Janus is in active development. Contributions are welcome.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Run tests (`pytest tests/`)
5. Submit a Pull Request

*See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.*

## License

MIT © 2026 · [LICENSE](LICENSE) · *Built on the insight that 3,000 years of human management wisdom is the best design manual for agent architectures.*
```

**设计理由：**
- **仅用一条 `---` 分隔线**——放在 Documentation 和 Contributing 之间，作为"正文→收口"的唯一硬分割。这是太极中阴阳之间的那一条 S 曲线——不是墙，是转场。
- License 和 Contributing 之间不用分隔线——它们都是轻量的"收口"信息，一起淡出。
- 尾部从 HTML `<p align="center"><sub>` 改为 License 段落末尾的斜体（淡墨），自然融入而无需 HTML。
- Documentation 表格中的文件名用粗体（浓墨），描述用纯文本（淡墨），层次清晰。

---

## 四、Markdown 太极美学表达规则

基于本次研究，总结出以下在 Markdown README 中应用的通用规则：

### 4.1 空行即是阴

| 呼吸等级 | 空行数 | 使用场景 |
|---------|--------|---------|
| **微呼吸** | 1 行 | 段落之间、列表项之间、机制条目之间 |
| **小呼吸** | 2 行 | 子章节之间、引用块前后 |
| **中呼吸** | 2-3 行 | 阳区之间（如 Quick Start → Core Mechanisms） |
| **大呼吸** | 3-4 行 | 重大转折（如 Hook → Why、Architecture → Quick Start） |
| **终呼吸** | 无内容 | 文末不留任何装饰，让目光自然落下 |

### 4.2 分隔线是刀，不是尺

- **尺（空行）** 测量节奏，让读者呼吸。
- **刀（`---`）** 切断关系，宣告"以下内容与此前无关"。
- **原则：** 一整篇 README 最多 1-2 条分隔线。只在"正文区→收口区"这种结构性断裂处使用。
- **禁用场景：** 两个语义相关的章节之间（如 Why → Architecture）、同一个阳区内的子节之间。

### 4.3 浓墨淡墨五色映射

| 太极色 | Markdown 表达 | 使用场景 |
|--------|-------------|---------|
| **浓墨** | `**粗体**` | 核心断言、关键概念首次出现、章节标题 |
| **淡墨** | `*斜体*` | 补充说明、脚注、引用来源、温和收束 |
| **青花** | 纯文本 + `` `code` `` | 架构说明、设计原理、技术细节 |
| **朱砂** | `**粗体**` + 否定句式 | 对比中的劣势、警告、反模式 |
| **泥金** | `**粗体**` + 肯定句式 | 成功标记、正面断言、安装成功的输出 |

### 4.4 引用块是呼吸框

引用块（`>`）在太极体系中是"柔"的容器——它不是强调，是**邀请读者停下来想一想**。

- **适合放：** 设计原则声明、核心哲学、一句话点睛
- **不适合放：** 实用信息（Requirements）、安装说明、技术约束
- **多行引用：** 用 `> ` + `>` 创建"引用块内的阴"——引用块内的空行。

示例：
```markdown
> **"Agent managing Agent should mirror Human managing Human."**
>
> This is not a metaphor. It's Janus's first design principle.
```

### 4.5 标题层级的纵深

- `#` 一级标题：仅用于项目名。一个 README 只有一个 `#`。
- `##` 二级标题：主要章节。不超过 8 个。
- `###` 三级标题：子章节。仅在 Core Mechanisms 或长篇章节中使用。
- **原则：** 二级标题的数量和间距直接决定 README 的"节奏"。8 个 `##` + 合理的呼吸区 = 舒适的阅读节奏。11 个 `##` + 每节一条分隔线 = 窒息。

### 4.6 HTML 是噪音

- 不用 `<p align="center">`、`<h3>`、`<sub>`、`<img>` 等 HTML 标签。
- shields.io 徽章如需保留，放底部 License 旁，单行纯 Markdown 链接形式。
- Markdown 的纯文本之力已经足够——相信它。

### 4.7 Unicode 框线字符

Janus CLI 框架使用的 `─│┌└` 等 Unicode 框线字符，在 README 的 Architecture ASCII 图中可以保留——它们是"青花"，是结构，不是装饰。

但注意：这些字符不要在正文段落中出现，只用于架构图等需要结构可视化的场景。

---

## 五、改进效果预测

| 指标 | 当前 | 改进后 |
|------|------|--------|
| `---` 分隔线 | 12 条 | 1 条 |
| HTML 标签 | 3 处 | 0 处 |
| 呼吸区（≥2行空行） | 0 个 | 6 个 |
| 引用块 | 2 处（1 处用错） | 3 处（全部正确） |
| 总行数（估算） | 212 行 | ~190 行 |
| 阅读节奏 | 碎片化、急促 | 三段式呼吸、张弛有度 |

### 五行平衡预估

```
当前五行分布：          改进后目标：
▓▓▓▓▓▓▓▓▓▓ 浓墨 40%    ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ 浓墨 25%
░░░░ 淡墨 10%           ░░░░░░░░░░░░░░░░░░░░░░░░░░ 淡墨 30%
████████████ 青花 45%   ██████████████████████████ 青花 35%
                        ·························· 留白 10%  ← 新增
```

改进后，浓墨从 40% 降到 25%（因为去掉了分隔线泛滥造成的"视觉重"），淡墨从 10% 升到 30%（引入更多斜体、呼吸感），留白从 0% 升到 10%（呼吸区）。青花（正文、代码块）保持主力地位。

---

## 六、实施优先级

按太极原则，改进应当**先做减法，再做加法**：

| 优先级 | 改动 | 影响 |
|--------|------|------|
| **P0** | 删除 11 条 `---` 分隔线，仅保留 1 条 | 即时提升呼吸感 |
| **P0** | 删除所有 HTML 标签（副标题、徽章、尾部） | 回归 Markdown 纯粹 |
| **P1** | Architecture 图前后加大呼吸（3 行空行） | 读者有时间消化架构 |
| **P1** | 重组布局为 6 个阳区，引入呼吸区体系 | 节奏从根本上改变 |
| **P2** | 淡墨化 Requirements / 尾部署名 | 细节精致化 |
| **P2** | 增加 Design Philosophy 引用块的多行呼吸 | 哲学区块更"柔" |
| **P3** | 如保留徽章，移至底部 License 旁 | 装饰退居末尾 |

---

*本文档是 Janus README 太极美学改进的完整设计方案。所有建议均可在纯 Markdown 中实现，无需外部工具、CSS 或构建步骤。*
