<!--
  发布前草稿。仓库地址 https://github.com/ZHUCH-520/grice-skill 是计划地址，尚未创建。
  各工具的目录和文档链接于 2026-10-31 逐个核对官方文档，来源见文末“资料来源”。
-->

# grice-skill：格莱斯合作原则 Agent Skill

**简体中文** | [English](#english)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-green)](https://agentskills.io)

这是一个依据格莱斯合作原则（Cooperative Principle）编写的 Agent Skill，用来规范 AI 助手回复和汇报时的表述。
它不修改代码、命令或数据，只规定助手怎样回答、怎样汇报。

## 格莱斯合作原则

格莱斯（H. P. Grice，1913–1988；又译格赖斯）是英国语言哲学家。合作原则是他 1967 年在哈佛大学 William James 讲座中提出的，1975 年以〈逻辑与会话〉（Logic and Conversation）为题发表。

这一理论设想：交谈各方被默认相互合作，认可某个共同的目的或方向。合作原则是这一设想的表述：

> 在交谈的每一阶段，说出这场交谈公认的目的或方向所要求的话。

它由数量、质量、关系、方式四类准则具体化，每类下有若干次准则，最初用来解释会话含义。下表中文据原文译出，术语参照通行的语用学教材。

| 准则 | 次准则（格莱斯，1975） | 本 skill 对助手的要求 |
|---|---|---|
| **数量准则**（Quantity） | ① 所说的话应包含当前交谈目的所需的信息。<br>② 所说的话不应包含超出需要的信息。 | 答案、结论、阻塞项放在第一句；读者下一步要用的命令、路径、数字都要给出；复述请求、过程叙述、收尾总结删去。 |
| **质量准则**（Quality） | 上位准则：力求所说的话真实。<br>① 不说自知虚假的话。<br>② 不说缺乏足够证据的话。 | 本轮没有亲眼看到证据的结论，写作“未验证”；不知道的写作“不知道”，不用猜测补全。 |
| **关系准则**（Relation） | 所说的话要相关。 | 回答被问的问题；用户的前提有误时，第一句指出。 |
| **方式准则**（Manner） | 上位准则：清楚明白地说。<br>① 避免晦涩。② 避免歧义。<br>③ 简练（避免不必要的冗长）。④ 有条理。 | 指代明确，时间带时区；“部分通过”“已处理”这类会被读出更强含义的说法，补写边界。 |

几点说明：
- 格莱斯自己指出，第二条数量准则有争议，其作用或可由关系准则达到。各准则的紧迫程度也不相同，违反质量准则比违反方式准则更严重。
- 方式准则关心的是话怎么说，其余三类关心说了什么。
- 会话含义（conversational implicature）指说话人没有明说、听者却能推出的意思。助手的回复同样会产生会话含义，例如“没发现问题”会被理解为“已全部检查”。

## 一个例子（数量准则 ①）

```text
问：可以上线了吗？
甲：迁移已运行，无报错。
乙：无报错，但 2 张表被跳过，需补跑。
注：甲省略上线所需的信息（数量准则 ①）。
```

甲所说属实，日志里确实没有报错；但读者会把“无报错”理解为“已全部完成”，据此上线。

## skill 包含什么

[`SKILL.md`](skills/grice-cooperative-principle/SKILL.md)（约 220 行）包含：四类准则及对助手的具体做法；会话含义对照表；违反、退出、冲突、故意违反四种“不遵守准则”的处理；准则冲突时的处理顺序；助手之间交接的模板；发送前的 8 条自检；8 个“差 → 好”的对照例子。
其中冲突处理顺序（质量准则优先于数量准则等）是本 skill 针对助手场景设定的，不是格莱斯的主张。

## 安装

### 方式一：让 AI 助手自行安装

打开你平时用的 AI 编程助手（Claude Code、Codex、Cursor、Trae、CodeBuddy、通义灵码、Qoder 等），发这一句：

```text
帮我安装这个 skill：https://github.com/ZHUCH-520/grice-skill/tree/main/skills/grice-cooperative-principle
```

装好后，重开一个新对话，再试一句：

```text
你现在装了哪些 skill？有没有 grice-cooperative-principle？
```

列表里有这个名字，即安装成功。之后无需额外操作，助手会在回复和汇报时自动使用。
想手动调用的话，在 Claude Code、Cursor 等支持斜杠命令的工具里输入 `/grice-cooperative-principle`；Codex 里输入 `$grice-cooperative-principle`。

> 助手无法安装，通常是因为它不能联网，或无法访问 GitHub。见下文“打不开 GitHub”。

### 方式二：用命令行安装

装进你电脑上已有的各种助手（会列出检测到的工具让你勾选）：

```bash
npx skills add ZHUCH-520/grice-skill
```

这是 [vercel-labs/skills](https://github.com/vercel-labs/skills) 这个通用安装器。它的文档里列出支持 Claude Code、Codex、Cursor、Gemini CLI、CodeBuddy、通义灵码（Lingma）、Qoder、Qwen Code、Trae、Trae CN、Kimi Code CLI 等。

只装 Gemini CLI：

```bash
gemini skills install https://github.com/ZHUCH-520/grice-skill.git --path skills/grice-cooperative-principle
```

### 方式三：手动复制（目录已按官方文档核对）

下面的目录，都是**各工具官方文档写明的** skill 目录。把 `skills/grice-cooperative-principle/` 整个文件夹复制进去就行，
文件夹名保持 `grice-cooperative-principle`。“用户级”对所有项目生效，“项目级”只对当前项目生效。

| 工具 | 原生支持 SKILL.md | 用户级目录 | 项目级目录 |
|---|---|---|---|
| Claude Code | 是 | `~/.claude/skills/` | `.claude/skills/` |
| OpenAI Codex CLI | 是 | `~/.agents/skills/` | `.agents/skills/` |
| Cursor | 是 | `~/.cursor/skills/` 或 `~/.agents/skills/` | `.cursor/skills/` 或 `.agents/skills/` |
| Gemini CLI | 是 | `~/.gemini/skills/` 或 `~/.agents/skills/` | `.gemini/skills/` 或 `.agents/skills/` |
| **Trae（国际版）** | 是 | `~/.trae/skills/` | `.trae/skills/` |
| **Trae（中文版）** | 是 | `~/.trae-cn/skills/` | `.trae/skills/` |
| **CodeBuddy（腾讯）** | 是 | `~/.codebuddy/skills/` | `.codebuddy/skills/` |
| **Qoder（阿里）IDE** | 是 | `~/.qoder/skills/` | `.qoder/skills/` |
| **Qoder CN CLI** | 是（项目级） | 文档未列出 | `.qoder/skills/` |
| **通义灵码 / Lingma（Qoder CN IDE）** | 是 | `~/.lingma/skills/` | `.lingma/skills/` |
| **Kimi Code CLI（月之暗面）** | 是 | `~/.kimi-code/skills/` 或 `~/.agents/skills/` | `.kimi-code/skills/` 或 `.agents/skills/` |
| **Qwen Code（通义千问）** | 是 | `~/.qwen/skills/` 或 `~/.agents/skills/` | `.qwen/skills/` 或 `.agents/skills/` |
| **DeepSeek Harness（`dsh`）** | 是 | `~/.agents/skills/`（见下方说明 ¹） | `.dsh/skills/` 或 `.agents/skills/` |
| **智谱 CodeGeeX** | 未找到 | — | 用下面的“规则文件版” |
| **智谱 GLM / Z.ai** | 不是工具，是模型套餐 | 在 Claude Code、Cursor、Trae、Qoder 等里用 GLM，就按那些工具装 | |

几点说明：

- **Trae** 的目录要分国际版和中文版：中文版用户级是 `~/.trae-cn/skills/`。也可以在 IDE 里 设置 → 技能与命令（Skills & Commands），直接上传 `SKILL.md` 或 zip。
  用 `.agents/skills/` 要先在设置里打开“启用 .agents 技能目录”。
- **Gemini CLI**：它的官方文档页顶部写着，免费用户和 Google One 用户的 Gemini CLI 已在 2026 年 6 月 18 日被 Antigravity CLI 取代。其他账号类型是否继续可用，页面没有写清。上表是 Gemini CLI 文档里的目录；Antigravity CLI 的 skill 目录我没有在官方文档里核对到，请以它自己的文档为准。
- **Qoder CN CLI**：官方配置页只写了项目级 `.qoder/skills/`，用户级目录没有列出，所以这里不写。
- **Qwen Code、Kimi Code CLI、Cursor、Codex、Gemini CLI** 都会读 `~/.agents/skills/`。想装一次、多个工具共用，就放这里。
- ¹ **DeepSeek Harness（`dsh`）**：官方仓库文档写明项目级 `.dsh/skills/`、`.agents/skills/` 会被扫描，用户级是 `<dshHome>/skills`（`~/.agents/skills/` 对应的 `<agentsHome>/skills`）。`~/.agents/skills/` 这个具体路径来自第三方指南 dshplugin.app，官方文档没有写出展开后的路径。`dsh` 要求 skill 名是小写加连字符，本 skill 符合。
- **MarsCode**：豆包 MarsCode 编程助手已在 2025 年 4 月改名为“Trae 插件”，并入 Trae 品牌。Trae 插件是否支持 skill 没有核对到，所以没列。用 Trae IDE 的话按上表装。
- **iFlow CLI**：官方已于 2026 年 4 月 17 日停止服务，不再推荐。

我核对的是各家文档里写的目录，**没有在每个工具里逐个实机跑过**。如果哪一行在你那里不灵，欢迎开 issue 告诉我。

### 方式四：工具不支持 skill 时，使用规则文件版

没有 skill 功能的工具（或者你只想要一份轻量的），把 [`snippets/rules-snippet.md`](snippets/rules-snippet.md) 里那一段（约 10 行，中英都有）粘进它的规则文件。放哪个文件：

| 工具 | 粘到哪里 |
|---|---|
| Claude Code | `CLAUDE.md`（项目）或 `~/.claude/CLAUDE.md`（所有项目） |
| OpenAI Codex CLI | `AGENTS.md` |
| Cursor | `.cursor/rules/` 下新建一个规则文件，或项目根的 `AGENTS.md` |
| Gemini CLI | `GEMINI.md` |
| Trae | `.trae/rules/` 下新建 `grice.md`，生效方式选“始终生效”（中文版文档的路径；国际版同名页面未能打开核对） |
| CodeBuddy | `CODEBUDDY.md` 或 `.codebuddy/rules/grice.md` |
| Qoder IDE | `.qoder/rules/` 下新建规则文件 |
| 通义灵码 / Qoder CN | `.lingma/rules/` 下新建规则文件 |
| Qwen Code | `QWEN.md` |
| Kimi Code CLI | 项目根的 `AGENTS.md`（文档称“工作区指令文件，如 AGENTS.md”） |
| 智谱 CodeGeeX | 官方文档里没找到对话规则文件。如果你在 CodeGeeX 里能设“自定义指令”，把那一段粘进去 |
| 其他 | 找到“规则 / 记忆 / 自定义指令 / system prompt”，把那一段粘进去 |

规则文件每次对话都会整段载入上下文，所以这一版刻意写短。需要会话含义对照表、冲突处理顺序和例子的，使用完整的 `SKILL.md`。

### 打不开 GitHub

1. **直接复制文字**（最稳）：在能打开的地方拿到 [`SKILL.md`](skills/grice-cooperative-principle/SKILL.md) 的全文，自己建文件夹 `grice-cooperative-principle`，把全文存成里面的 `SKILL.md`，放进上表对应的目录。然后跟助手说：“帮我安装这个本地 skill 文件夹：<文件夹路径>”。
2. **下载压缩包**：在仓库页点 Code → Download ZIP，解压后把 `skills/grice-cooperative-principle` 这个文件夹复制过去。
3. **Gitee 镜像**：计划中，还没建。建好后会把地址写在这里。
4. 如果你有自己信得过的 GitHub 加速服务，也可以拿它下载 ZIP。第三方加速站不在本项目维护范围内，也可能随时失效。

## 文件

```text
grice-skill/
├── skills/
│   └── grice-cooperative-principle/
│       ├── SKILL.md              # skill 本体
│       └── references/
│           └── SOURCES.md        # 来源：原文、综述、AI 相关研究
├── snippets/
│   └── rules-snippet.md          # 规则文件版（AGENTS.md / CLAUDE.md 等用）
├── README.md
└── LICENSE                       # MIT
```

## 说明与局限

- skill 能让助手更守规矩，不能保证每次都做到。发现某条回复有问题，可以把它发给助手，指出违反了哪条准则，助手通常会改正。
- 格莱斯的原文只有合作原则和四类准则。“质量准则优先于数量准则”等冲突处理顺序，是为 AI 助手场景设定的，不是格莱斯的主张。来源和这一区分见 [`references/SOURCES.md`](skills/grice-cooperative-principle/references/SOURCES.md)。
- 合作原则预设交谈各方目标一致，对争辩、玩笑、礼貌等场景的解释力有限。skill 的 “边界” 一节说明了这一点。
- skill 用中文写成，助手会按你对话使用的语言回复。需要英文版的，欢迎提交 PR。
- 创作、闲聊类的回复，数量准则和方式准则可以放宽，skill 中已写明。

## 许可

[MIT](LICENSE)。可自由使用、修改和分发。

## 资料来源（各工具官方文档，2026-10-31 核对）

<!-- 每一行对应上面表格的一行。核对方式：打开页面，读到目录或配置的原文。 -->

- Claude Code：https://code.claude.com/docs/en/skills 、https://code.claude.com/docs/en/memory
- Codex：https://developers.openai.com/codex/skills 、https://developers.openai.com/codex/guides/agents-md
- Cursor：https://cursor.com/docs/skills 、https://cursor.com/docs/context/rules
- Gemini CLI：https://geminicli.com/docs/cli/skills/ 、https://geminicli.com/docs/cli/gemini-md/
- Trae 国际版：https://docs.trae.ai/ide/skills
- Trae 中文版：https://docs.trae.cn/ide/skills 、https://docs.trae.cn/ide/rules
- CodeBuddy：https://www.codebuddy.cn/docs/cli/skills 、https://www.codebuddy.cn/docs/cli/memory
- Qoder：https://docs.qoder.com/extensions/skills 、https://docs.qoder.com/user-guide/rules
- Qoder CN CLI：https://docs.qoder.cn/cli/config-scope
- 通义灵码 / Lingma（Qoder CN IDE）：https://docs.qoder.cn/user-guide/skills 、https://docs.qoder.cn/user-guide/rules
- Kimi Code CLI：https://www.kimi.com/code/docs/kimi-code-cli/customization/skills.html 、https://www.kimi.com/code/docs/kimi-code-cli/customization/agents.html
- Qwen Code：https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/ 、https://qwenlm.github.io/qwen-code-docs/en/users/configuration/settings/
- DeepSeek Harness：https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/skill/skill-filesystem/README.md ；第三方指南：https://dshplugin.app/guides/deepseek-harness-skills
- 通用安装器 `skills`：https://github.com/vercel-labs/skills （支持的工具和目录：`docs/agents.md`）
- iFlow CLI 停服：https://vibex.iflow.cn/t/topic/4819 、https://vibex.iflow.cn/t/topic/5753
- MarsCode 改名 Trae 插件：https://juejin.cn/pin/7493483744562495522
- 智谱：https://docs.bigmodel.cn/cn/managed-agents/skills （云端 Agent 的 skill，不是 CodeGeeX 插件）、https://docs.z.ai/devpack/tool/others

---

<a id="english"></a>

# grice-skill: an Agent Skill based on Grice's Cooperative Principle

[简体中文](#grice-skill格莱斯合作原则-agent-skill) | **English**

An Agent Skill based on the Cooperative Principle, for governing how an AI assistant words its replies and status reports.
It changes nothing about your code, commands or data. It only specifies how the assistant answers and reports.

## The Cooperative Principle

H. P. Grice (1913–1988) was a British philosopher of language. He proposed the Cooperative Principle in his 1967 William James Lectures at Harvard, and published it in 1975 as "Logic and Conversation".

The theory assumes that the parties to a conversation are cooperating: they recognise some common purpose or direction. The principle states that assumption:

> Make your conversational contribution such as is required, at the stage at which it occurs, by the accepted purpose or direction of the talk exchange in which you are engaged.

It is made specific by four categories of maxims (Quantity, Quality, Relation, Manner), each with sub-maxims, and it was introduced to explain conversational implicature. The wording below follows Grice's text.

| Category | Maxims (Grice, 1975) | What this skill asks of the assistant |
|---|---|---|
| **Quantity** | 1. Make your contribution as informative as is required (for the current purposes of the exchange).<br>2. Do not make your contribution more informative than is required. | Put the answer, conclusion or blocker first; include the command, path or number the reader needs next; drop restated requests, narrated process and closing summaries. |
| **Quality** | Supermaxim: try to make your contribution one that is true.<br>1. Do not say what you believe to be false.<br>2. Do not say that for which you lack adequate evidence. | A conclusion without evidence from this turn is reported as "not verified". What the assistant does not know is reported as unknown, not filled in with a guess. |
| **Relation** | Be relevant. | Answer the question that was asked. If the user's premise is wrong, say so in the first sentence. |
| **Manner** | Supermaxim: be perspicuous.<br>1. Avoid obscurity of expression.<br>2. Avoid ambiguity.<br>3. Be brief (avoid unnecessary prolixity).<br>4. Be orderly. | Unambiguous references, times with a timezone. Weak wording such as "some tests passed" or "handled" invites a stronger reading, so state the boundary. |

Notes:
- Grice himself called the second Quantity maxim disputable, and said its effect might be secured by the Relation maxim. He also said the maxims differ in urgency: breaching Quality is worse than breaching Manner.
- Manner concerns how something is said; the other three categories concern what is said.
- Conversational implicature is what a speaker conveys without stating it. An assistant's replies produce implicatures too; "no issues found" is heard as "everything was checked".

## An example (Quantity, maxim 1)

```text
Q: Is it ready to go live?
A: The migration ran with no errors.
B: No errors, but 2 tables were skipped and need to be re-run.
Note: A omits information needed for the decision (Quantity, maxim 1).
```

A's statement is true: the log shows no error. But the reader takes "no errors" to mean "everything completed" and goes live.

## What the skill contains

[`SKILL.md`](skills/grice-cooperative-principle/SKILL.md) (about 220 lines, written in Chinese; the assistant replies in the language you use) contains: the four categories with concrete behaviour for an assistant; an implicature table; how to treat the four ways of not observing a maxim (violate, opt out, clash, flout); an order of priority for clashes; a handoff template for passing work to another agent; an 8-point pre-send check; and 8 before/after examples.
The order of priority for clashes (Quality over Quantity, and so on) was set for the assistant setting. It is not Grice's own claim.

## Install

### Option 1: ask your assistant to install it

In Claude Code, Codex, Cursor, Trae, CodeBuddy, Qoder, Qwen Code, Kimi Code CLI or similar, say:

```text
Install this skill for me: https://github.com/ZHUCH-520/grice-skill/tree/main/skills/grice-cooperative-principle
```

Then start a new conversation and ask "which skills do you have?". If `grice-cooperative-principle` is listed, you're done.

### Option 2: command line

```bash
npx skills add ZHUCH-520/grice-skill
```

This uses the generic [vercel-labs/skills](https://github.com/vercel-labs/skills) installer, which lists support for Claude Code, Codex, Cursor, Gemini CLI, CodeBuddy, Lingma, Qoder, Qwen Code, Trae, Kimi Code CLI and more. For Gemini CLI alone:

```bash
gemini skills install https://github.com/ZHUCH-520/grice-skill.git --path skills/grice-cooperative-principle
```

### Option 3: copy the folder

Copy `skills/grice-cooperative-principle/` into the skills directory of your tool. The directories in the table above (Chinese section) come from each tool's official documentation, checked on 2026-10-31. Short version: Claude Code `~/.claude/skills/`, Codex / Cursor / Gemini CLI / Qwen Code / Kimi Code CLI `~/.agents/skills/` (also read by several others), Trae `~/.trae/skills/` (China edition `~/.trae-cn/skills/`), CodeBuddy `~/.codebuddy/skills/`, Qoder `~/.qoder/skills/`, Lingma `~/.lingma/skills/`, Qwen Code `~/.qwen/skills/`, DeepSeek Harness `.dsh/skills/` or `.agents/skills/` in the project. I checked the documented paths; I did not run every tool end to end.

### Option 4: no skill support? Use the rules snippet

Paste the block in [`snippets/rules-snippet.md`](snippets/rules-snippet.md) (about 10 lines, Chinese and English) into `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `QWEN.md`, `CODEBUDDY.md`, or the tool's rules directory (`.cursor/rules/`, `.trae/rules/`, `.qoder/rules/`, `.lingma/rules/`).

### Can't reach GitHub?

Copy the text of `SKILL.md` into a folder named `grice-cooperative-principle` in the right directory; or download the ZIP from a machine that can reach GitHub. A Gitee mirror is planned but not set up yet.

## Notes

- A skill makes an assistant more disciplined; it does not guarantee it. If a reply slips, quote it back and name the maxim it broke.
- Grice's text contains the Cooperative Principle and four categories of maxims. The conflict priority "Quality over Quantity" was set for AI assistants and is not Grice's claim. See [`references/SOURCES.md`](skills/grice-cooperative-principle/references/SOURCES.md).
- The principle assumes the parties share a purpose, and explains argument, joking and politeness less well. Creative writing and chit-chat relax Quantity and Manner; the skill says so.

## License

[MIT](LICENSE).
