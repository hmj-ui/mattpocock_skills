<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# Skills For Real Engineers

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

My agent skills that I use every day to do real engineering - not vibe coding.

Developing real applications is hard. Approaches like GSD, BMAD, and Spec-Kit try to help by owning the process. But while doing so, they take away your control and make bugs in the process hard to resolve.

These skills are designed to be small, easy to adapt, and composable. They work with any model. They're based on decades of engineering experience. Hack around with them. Make them your own. Enjoy.

If you want to keep up with changes to these skills, and any new ones I create, you can join ~60,000 other devs on my newsletter:

[Sign Up To The Newsletter](https://www.aihero.dev/s/skills-newsletter)

## Installation (30-second setup)

Two ways in, two philosophies. **The [Claude Code plugin](https://code.claude.com/docs/en/plugins)** installs the whole set as a managed, read-only bundle that updates when I ship, so you subscribe rather than fork. **[skills.sh](https://skills.sh/mattpocock/skills)** copies editable skill files into your project, so you can hack on them and make them your own. Pick one: installing both leaves you with every skill twice.

### 1. Get the skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

Or, from inside a session:

```
/plugin install mattpocock-skills
```

It's in Claude Code's official marketplace, so there's nothing to add first, and updates arrive automatically.

</details>

<details>
<summary><strong>Codex, and other agents</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

Pick the skills you want, and which coding agents to install them on. **The installer lets you choose which skills to take, so make sure `setup-matt-pocock-skills` is one of them.**

A native Codex plugin is on the roadmap (see [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)).

</details>

<details>
<summary><strong>For tinkerers</strong></summary>

Use the same installer, on any agent, including Claude Code:

```bash
npx skills@latest add mattpocock/skills
```

It writes the skills into your repo as ordinary files you own and can edit. Nothing updates behind your back; pull my latest changes when you want them with `npx skills update`.

</details>

### 2. Run `/setup-matt-pocock-skills`

In your agent, run it once per repo. It will:

- Ask you which issue tracker you want to use (GitHub, Linear, or local files)
- Ask you what labels you apply to tickets when you triage them (`/triage` uses labels)
- Ask you where you want to save any docs we create

### 3. Bam - you're ready to go.

## Why These Skills Exist

I built these skills as a way to fix common failure modes I see with Claude Code, Codex, and other coding agents.

### #1: The Agent Didn't Do What I Want

> "No-one knows exactly what they want"
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**. The most common failure mode in software development is misalignment. You think the dev knows what you want. Then you see what they've built - and you realize it didn't understand you at all.

This is just the same in the AI age. There is a communication gap between you and the agent. The fix for this is a **grilling session** - getting the agent to ask you detailed questions about what you're building.

**The Fix** is to use:

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) - for non-code uses
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) - same as [`/grill-me`](./skills/productivity/grill-me/SKILL.md), but adds more goodies (see below)

These are my most popular skills. They help you align with the agent before you get started, and think deeply about the change you're making. Use them _every_ time you want to make a change.

### #2: The Agent Is Way Too Verbose

> With a ubiquitous language, conversations among developers and expressions of the code are all derived from the same domain model.
>
> Eric Evans, [Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**The Problem**: At the start of a project, devs and the people they're building the software for (the domain experts) are usually speaking different languages.

I felt the same tension with my agents. Agents are usually dropped into a project and asked to figure out the jargon as they go. So they use 20 words where 1 will do.

**The Fix** for this is a shared language. It's a document that helps agents decode the jargon used in the project.

<details>
<summary>
Example
</summary>

Here's an example [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md), from my `course-video-manager` repo. Which one is easier to read?

- **BEFORE**: "There's a problem when a lesson inside a section of a course is made 'real' (i.e. given a spot in the file system)"
- **AFTER**: "There's a problem with the materialization cascade"

This concision pays off session after session.

</details>

This is built into [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md). It's a grilling session, but that helps you build a shared language with the AI, and document hard-to-explain decisions in ADR's.

It's hard to explain how powerful this is. It might be the single coolest technique in this repo. Try it, and see.

> [!TIP]
> A shared language has many other benefits than reducing verbosity:
>
> - **Variables, functions and files are named consistently**, using the shared language
> - As a result, the **codebase is easier to navigate** for the agent
> - The agent also **spends fewer tokens on thinking**, because it has access to a more concise language

### #3: The Code Doesn't Work

> "Always take small, deliberate steps. The rate of feedback is your speed limit. Never take on a task that’s too big."
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**: Let's say that you and the agent are aligned on what to build. What happens when the agent _still_ produces crap?

It's time to look at your feedback loops. Without feedback on how the code it produces actually runs, the agent will be flying blind.

**The Fix**: You need the usual tranche of feedback loops: static types, browser access, and automated tests.

For automated tests, a red-green-refactor loop is critical. This is where the agent writes a failing test first, then fixes the test. This helps give the agent a consistent level of feedback that results in far better code.

I've built a **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill** you can slot into any project. It encourages red-green-refactor and gives the agent plenty of guidance on what makes good and bad tests.

For debugging, I've also built a **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill that wraps best debugging practices into a disciplined loop, gated phase by phase.

### #4: We Built A Ball Of Mud

> "Invest in the design of the system _every day_."
>
> Kent Beck, [Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "The best modules are deep. They allow a lot of functionality to be accessed through a simple interface."
>
> John Ousterhout, [A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**The Problem**: Most apps built with agents are complex and hard to change. Because agents can radically speed up coding, they also accelerate software entropy. Codebases get more complex at an unprecedented rate.

**The Fix** for this is a radical new approach to AI-powered development: caring about the design of the code.

This is built in to every layer of these skills:

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) quizzes you about which modules you're touching before creating a spec

And crucially, [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) surveys a codebase for deepening opportunities and hands you the candidates. I recommend running it on your codebase once every few days. It is a survey, not a rescue: on a genuinely old codebase it will find real candidates, but it won't untangle the mud for you.

### Summary

Software engineering fundamentals matter more than ever. These skills are my best effort at condensing these fundamentals into repeatable practices, to help you ship the best apps of your career. Enjoy.

## Reference

These split on one axis: who can invoke them. **User-invoked** skills are reachable only when you type them (e.g. `/grill-me`); their job is to orchestrate. **Model-invoked** skills can be invoked by you _or_ reached for automatically by the agent when the task fits; they hold the reusable discipline. A user-invoked skill may invoke model-invoked skills, but never another user-invoked one.

### Engineering

Skills I use daily for code work.

**User-invoked**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**: Ask which skill or flow fits your situation. A router over the user-invoked skills in this repo.
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: Grilling session that also builds your project's domain model, sharpening terminology and updating `CONTEXT.md` and ADRs inline.
- **[triage](./skills/engineering/triage/SKILL.md)**: Move issues through a state machine of triage roles.
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: Scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**: Configure this repo for the engineering skills (issue tracker, triage labels, domain doc layout). Run once per repo before using the other engineering skills.
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: Turn the current conversation into a spec and publish it to the issue tracker. No interview, just synthesizes what you've already discussed.
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: Break any plan, spec, or conversation into a set of tracer-bullet tickets, each declaring its blocking edges, written as text in a local file, or as native blocking links on a real tracker.
- **[implement](./skills/engineering/implement/SKILL.md)**: Build the work described by a spec or set of tickets, driving `/tdd` at pre-agreed seams and closing out with `/code-review` before committing.
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: Plan a huge chunk of work, more than one agent session can hold, as a shared map of decision tickets on the issue tracker, and resolve them one at a time until the way to the destination is clear.

**Model-invoked**

- **[prototype](./skills/engineering/prototype/SKILL.md)**: Build a throwaway prototype to answer a design question, either a single shareable HTML file for state/logic questions, or several radically different UI variations toggleable from one route.
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: Disciplined diagnosis loop for hard bugs and performance regressions: build a feedback loop that goes red on this bug → minimise → hypothesise → instrument → fix → regression-test.
- **[research](./skills/engineering/research/SKILL.md)**: Investigate a question against high-trust primary sources and capture the findings as a cited Markdown file in the repo, run as a background agent.
- **[tdd](./skills/engineering/tdd/SKILL.md)**: Test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**: Actively build and sharpen a project's domain model: challenge terms against the glossary, stress-test with edge-case scenarios, and update `CONTEXT.md` and ADRs inline.
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: Shared discipline and vocabulary for designing deep modules: a lot of behaviour behind a small interface, placed at a clean seam, testable through that interface.
- **[code-review](./skills/engineering/code-review/SKILL.md)**: Two-axis review of the diff since a fixed point: **Standards** (does it follow the repo's coding standards, plus a Fowler smell baseline?) and **Spec** (does it faithfully implement the originating issue/spec?), run as parallel sub-agents so neither pollutes the other.
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)**: Work through an in-progress git merge or rebase conflict hunk by hunk, resolving by intent traced to each side's primary source, then finish the operation (never `--abort`).
- **[wizard](./skills/engineering/wizard/SKILL.md)**: Generate an interactive bash wizard that walks a human through steps only they can perform: provisioning infrastructure, setting up credentials or CI secrets, walking an unfamiliar third-party dashboard, or running a one-off migration or cutover.

### Productivity

General workflow tools, not code-specific.

**User-invoked**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**: Get relentlessly interviewed about a plan or design until every branch of the design tree is resolved.
- **[handoff](./skills/productivity/handoff/SKILL.md)**: Compact the current conversation into a handoff document so another agent can continue the work.
- **[teach](./skills/productivity/teach/SKILL.md)**: Teach the user a new skill or concept over multiple sessions, using the current directory as a stateful teaching workspace.
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**: Turn a decision you can't answer alone into a Markdown questionnaire for the one person who can, filled in async, or together over a meeting. It grills you about the send (who it's for, what you need back), not the subject.
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**: Fire this the moment a message doesn't land. The agent re-pitches it with the context you're missing, in plain English, using your `CONTEXT.md` vocabulary.

**Model-invoked**

- **[grilling](./skills/productivity/grilling/SKILL.md)**: Interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved. The reusable interview primitive behind `grill-me`, `grill-with-docs`, `triage`, `wayfinder` and `improve-codebase-architecture`.
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**: Writing documents for agents: skills, AGENTS.md/CLAUDE.md, and any doc an agent reaches by a pointer.

---

<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 面向真正工程师的技能（Skills）

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

我每天用来做真正工程的智能体技能，而不是 vibe coding（凭感觉编程）。

开发真正的应用很难。像 GSD、BMAD 和 Spec-Kit 这类方法试图通过接管整个流程来帮忙，但这样做的同时，它们也夺走了你的控制权，让流程中的 bug 难以解决。

这些技能被设计得小巧、易于改编、可组合。它们适用于任何模型，基于数十年的工程经验。随意折腾它们，把它们变成你自己的。享受其中。

如果你想跟上这些技能的变化以及我创建的新技能，可以加入我的通讯，已经有约 6 万名开发者订阅：

[订阅通讯](https://www.aihero.dev/s/skills-newsletter)

## 安装（30 秒搞定）

两条路径，两种理念。**[Claude Code 插件](https://code.claude.com/docs/en/plugins)** 把整套技能作为一个托管、只读的包来安装，随我发布自动更新，所以你是订阅而不是 fork。**[skills.sh](https://skills.sh/mattpocock/skills)** 则把可编辑的技能文件复制到你的项目里，你可以随意修改，把它们变成你自己的。二选一：两种都装会让每个技能出现两次。

### 1. 获取技能

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者在会话内：

```
/plugin install mattpocock-skills
```

它已收录在 Claude Code 官方市场里，所以无需先添加市场，更新会自动到来。

</details>

<details>
<summary><strong>Codex 及其他智能体</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

选择你想要的技能以及要安装到哪些编码智能体上。**安装器允许你选择要哪些技能，请务必把 `setup-matt-pocock-skills` 选上。**

原生 Codex 插件在路线图上（见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)）。

</details>

<details>
<summary><strong>给爱折腾的人</strong></summary>

在任何智能体上（包括 Claude Code）使用同一个安装器：

```bash
npx skills@latest add mattpocock/skills
```

它把技能以普通文件的形式写进你的仓库，你拥有并可以编辑它们。不会有任何背后自动更新；想拉取我的最新改动时，运行 `npx skills update` 即可。

</details>

### 2. 运行 `/setup-matt-pocock-skills`

在你的智能体里，每个仓库运行一次。它会：

- 询问你想用哪个 issue 跟踪器（GitHub、Linear，或本地文件）
- 询问你在 triage（分流）issue 时会打哪些标签（`/triage` 会用到标签）
- 询问你想把我们创建的任何文档保存在哪里

### 3. 搞定，可以开工了。

## 这些技能为何存在

我构建这些技能是为了修复我在 Claude Code、Codex 和其他编码智能体上看到的常见失败模式。

### #1：智能体没做我想要的

> "没有人确切知道自己想要什么。"
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》》

**问题**。软件开发中最常见的失败模式是对齐错位。你以为开发者知道你想要什么，然后你看到他们构建的东西，才发现它根本没理解你。

在 AI 时代同样如此。你与智能体之间存在沟通鸿沟。解决办法是一场**盘问式访谈（grilling session）**，让智能体就你要构建的东西向你提出详细的问题。

**解决办法**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md)，用于非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)，与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但增加了更多功能（见下）

这些是我最受欢迎的技能。它们帮助你在动手之前与智能体对齐，并深入思考你要做的改动。每次想做一个改动时都该用它们。

### #2：智能体太啰嗦

> 有了统一语言，开发者之间的交流以及代码的表达，都源自同一个领域模型。
>
> Eric Evans，《[领域驱动设计](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》》

**问题**：在项目初期，开发者和他们为之构建软件的人（领域专家）通常说着不同的语言。

我对我的智能体也有同样的感觉。智能体通常被丢进一个项目里，被要求自己摸索其中的术语。于是它用 20 个词来表达 1 个词就能说清的事。

**解决办法**是一种共享语言。这是一份帮助智能体解码项目中术语的文档。

<details>
<summary>
示例
</summary>

这是一个 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 的例子，来自我的 `course-video-manager` 仓库。哪个更容易读？

- **之前**："当课程某个章节里的一节课被'落实'（即在文件系统中获得一个位置）时，会出问题。"
- **之后**："materialization cascade 有问题。"

这种简洁性在一个又一个会话中持续受益。

</details>

这被内置在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 里。它是一场盘问式访谈，但帮助你与 AI 建立共享语言，并以 ADR 的形式记录难以解释的决策。

很难解释这有多强大。它可能是这个仓库里最酷的单个技术。试试看就知道了。

> [!TIP]
> 共享语言除了减少啰嗦之外，还有很多其他好处：
>
> - **变量、函数和文件会一致地命名**，使用共享语言
> - 结果是，**代码库对智能体更易导航**
> - 智能体也**在思考上花费更少的 token**，因为它能用更简洁的语言

### #3：代码不能用

> "总是迈出细小、刻意的步伐。反馈的频率就是你的速度上限。永远不要承担一个太大的任务。"
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》》

**问题**：假设你和智能体已经对齐了要构建什么。当智能体**仍然**产出垃圾时怎么办？

是时候审视你的反馈回路了。没有关于它产出的代码如何运行的反馈，智能体就是在盲飞。

**解决办法**：你需要通常的那一套反馈回路：静态类型、浏览器访问，以及自动化测试。

对于自动化测试，红-绿-重构（red-green-refactor）回路至关重要。智能体先写一个失败的测试，然后修复它。这给智能体提供一致的反馈水平，从而产出好得多的代码。

我构建了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 技能**，可以插入任何项目。它鼓励红-绿-重构，并给智能体大量指导，说明什么是好测试和坏测试。

对于调试，我还构建了一个 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** 技能，把最佳调试实践包装成一个有纪律的循环，逐阶段把关。

### #4：我们堆出了一个泥球

> "每天都要在系统设计上投资。"
>
> Kent Beck，《[解析极限编程](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》》

> "最好的模块是深的。它们允许通过简单的接口访问大量功能。"
>
> John Ousterhout，《[软件设计哲学](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》》

**问题**：用智能体构建的大多数应用都复杂且难以修改。因为智能体能极大地加速编码，它们也加速了软件熵。代码库以前所未有的速度变得更复杂。

**解决办法**是一种面向 AI 开发的全新思路：关心代码的设计。

这被内置在这些技能的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在创建 spec 之前会考你将触及哪些模块

而至关重要的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 会扫描代码库寻找"加深"机会，并把候选者交给你。我建议每隔几天在你的代码库上运行一次。它是一次扫描，而不是一次救援：在一个真正老旧的代码库上它会找到真正的候选者，但它不会替你解开泥球。

### 总结

软件工程基本功比以往任何时候都更重要。这些技能是我将基本功凝练成可重复实践的最佳尝试，帮助你交付职业生涯中最好的应用。享受其中。

## 参考

它们沿一个轴划分：谁能调用。**用户调用（User-invoked）**的技能只能在你输入名称时触达（例如 `/grill-me`），它们的工作是编排。**模型调用（Model-invoked）**的技能可以由你触达，也可以在任务匹配时被智能体自动调用，它们承载可复用的纪律。一个用户调用的技能可以调用模型调用的技能，但绝不能调用另一个用户调用的技能。

### Engineering（工程）

我每天用于代码工作的技能。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**：询问哪个技能或流程适合你的情况。本仓库用户调用技能之上的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**：盘问式访谈，同时构建项目的领域模型，磨锐术语并内联更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)**：把 issue 在 triage 角色的状态机中流转。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**：扫描代码库寻找加深机会，以可视化 HTML 报告呈现，然后盘问式访谈你选中的那一个。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**：为本仓库的工程技能做配置（issue 跟踪器、triage 标签、领域文档布局）。在使用其他工程技能之前每个仓库运行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**：把当前对话变成 spec 并发布到 issue 跟踪器。没有访谈，只是综合你已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**：把任何计划、spec 或对话拆解成一组 tracer-bullet（示踪弹）ticket，每个声明其阻塞边，以本地文件中的文本形式，或以真实跟踪器上的原生阻塞链接形式。
- **[implement](./skills/engineering/implement/SKILL.md)**：构建由 spec 或一组 ticket 描述的工作，在预先约定的接缝处驱动 `/tdd`，并在提交前以 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**：把一块巨大的工作（超过一个智能体会话所能容纳）规划为 issue 跟踪器上的一张共享决策 ticket 地图，逐一解决它们，直到通往目的地的路清晰。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)**：构建一次性原型来回答一个设计问题，可以是用于状态/逻辑问题的单个可分享 HTML 文件，也可以是从一个路由切换的几个截然不同的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**：针对疑难 bug 和性能回归的有纪律诊断循环：构建一个对这个 bug 变红的反馈回路 → 最小化 → 提出假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)**：针对高可信原始来源调查一个问题，并把发现以带引用的 Markdown 文件形式留在仓库里，作为后台智能体运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)**：以红-绿-重构循环进行的测试驱动开发。一次构建一个垂直切片的功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**：主动构建并磨锐项目的领域模型：用术语表挑战术语，用边缘场景压力测试，并内联更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**：设计深模块的共享纪律和词汇：大量行为隐藏在小接口背后，放在干净的接缝处，可通过该接口测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)**：对自某个固定点以来的 diff 做双轴审查：**标准**（是否遵循仓库的编码标准，加上 Fowler 的坏味基线？）和 **Spec**（是否忠实地实现了源自的 issue/spec？），作为并行子智能体运行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)**：逐 hunk 地处理进行中的 git merge 或 rebase 冲突，按追溯到双方原始来源的**意图**解决，然后完成操作（绝不 `--abort`）。
- **[wizard](./skills/engineering/wizard/SKILL.md)**：生成一个交互式 bash 向导，引导人类完成只有他们能做的步骤：配置基础设施、设置凭据或 CI 密钥、走完一个不熟悉的第三方控制台，或运行一次性的迁移或切换。

### Productivity（生产力）

通用工作流工具，与代码无关。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**：被 relentlessly（穷追不舍地）访谈关于一个计划或设计，直到设计树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)**：把当前对话压缩成一份交接文档，以便另一个智能体继续工作。
- **[teach](./skills/productivity/teach/SKILL.md)**：跨越多个会话教用户一个新技能或概念，使用当前目录作为有状态的教学习作区。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**：把你一个人无法回答的决策变成一份 Markdown 问卷，发给唯一能回答的那个人，异步填写，或一起在会议上填。它盘问你的是这次发送（发给谁、需要什么回来），而不是主题本身。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**：在一条消息没被理解的那一刻触发它。智能体用你缺失的上下文，用大白话，使用你的 `CONTEXT.md` 词汇重新讲述一遍。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)**：就一个计划、决策或想法穷追不舍地访谈用户，直到设计树的每个分支都被解决。`grill-me`、`grill-with-docs`、`triage`、`wayfinder` 和 `improve-codebase-architecture` 背后可复用的访谈原语。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**：为智能体写文档：技能、AGENTS.md/CLAUDE.md，以及任何智能体通过指针触达的文档。
