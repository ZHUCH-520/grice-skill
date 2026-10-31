<!--
  发布前草稿。仓库地址 https://github.com/ZHUCH-520/grice-skill 是计划地址，尚未创建。
  各工具的目录和文档链接于 2026-10-31 逐个核对官方文档，来源见文末“资料来源”。
-->

# grice-skill · 让 AI 助手说话像靠谱的同事

**简体中文** | [English](#english)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-SKILL.md-green)](https://agentskills.io)

一个只管“怎么说话”的 skill，基于格莱斯（H. P. Grice）的合作原则：**说够、说真、说对题、说清楚。**
装上以后，你的 AI 助手汇报工作时，不再“应该没问题”“部分通过”“已处理”地含糊过去。

**不装：**

> 部署完成。新版本已上线，监控正常。

**装了：**

> 新版本已部署，但“预热缓存”这一步超时失败（`warmup.sh` 退出码 124），缓存是冷的，首批请求会慢。监控只看了 2 分钟，没发现错误率上升。我可以重跑预热，要吗？

它不改代码，不改命令，不改数据，只管助手怎么回你的话。

## 四条准则，各管一件事

| 准则 | 一句话 | 助手该做的 |
|---|---|---|
| **量** | 说够，别多说 | 答案放第一句；下一步要用的命令、路径、数字都在；复述和收尾总结删掉 |
| **质** | 说真的 | 没亲眼看到证据，就写“未验证”；不知道就说不知道，不拿猜测补空 |
| **关系** | 说对题 | 答你问的，不答邻近的；你的前提有错，第一句就指出来 |
| **方式** | 说清楚 | 指代明确，时间带时区；“部分通过”这种会被读错的说法，补上边界 |

另外还有：会话含意对照表（“没发现问题”会被听成“已全部检查”）、准则冲突时谁优先（质 > 量）、
交接给另一个助手时必须写清哪些事、发送前 8 条自检，以及 8 个“差 → 好”的对照例子。
全部在 [`SKILL.md`](skills/grice-cooperative-principle/SKILL.md) 里，大约 220 行。

## 安装

### 最简单的办法：让你的 AI 助手自己装

打开你平时用的 AI 编程助手（Claude Code、Codex、Cursor、Trae、CodeBuddy、通义灵码、Qoder……都行），发这一句：

```text
帮我安装这个 skill：https://github.com/ZHUCH-520/grice-skill/tree/main/skills/grice-cooperative-principle
```

装好后，重开一个新对话，再试一句：

```text
你现在装了哪些 skill？有没有 grice-cooperative-principle？
```

它能说出这个名字，就装好了。之后你什么都不用做，助手会在回复和汇报时自己用。
想手动调用的话，在 Claude Code、Cursor 等支持斜杠命令的工具里输入 `/grice-cooperative-principle`；Codex 里输入 `$grice-cooperative-principle`。

> 助手装不上，多半是它不能联网，或者打不开 GitHub。往下看“打不开 GitHub”。

### 用命令行装

装进你电脑上已有的各种助手（会列出检测到的工具让你勾选）：

```bash
npx skills add ZHUCH-520/grice-skill
```

这是 [vercel-labs/skills](https://github.com/vercel-labs/skills) 这个通用安装器。它的文档里列出支持 Claude Code、Codex、Cursor、Gemini CLI、CodeBuddy、通义灵码（Lingma）、Qoder、Qwen Code、Trae、Trae CN、Kimi Code CLI 等。

只装 Gemini CLI：

```bash
gemini skills install https://github.com/ZHUCH-520/grice-skill.git --path skills/grice-cooperative-principle
```

### 各工具怎么装（手动，核对过官方文档）

下面的目录，都是**各工具官方文档写明的** skill 目录。把 `skills/grice-cooperative-principle/` 整个文件夹复制进去就行，
文件夹名保持 `grice-cooperative-principle`。“用户级”对所有项目生效，“项目级”只对当前项目生效。

| 工具 | 原生支持 SKILL.md | 用户级目录 | 项目级目录 |
|---|---|---|---|
| Claude Code | ✅ | `~/.claude/skills/` | `.claude/skills/` |
| OpenAI Codex CLI | ✅ | `~/.agents/skills/` | `.agents/skills/` |
| Cursor | ✅ | `~/.cursor/skills/` 或 `~/.agents/skills/` | `.cursor/skills/` 或 `.agents/skills/` |
| Gemini CLI | ✅ | `~/.gemini/skills/` 或 `~/.agents/skills/` | `.gemini/skills/` 或 `.agents/skills/` |
| **Trae（国际版）** | ✅ | `~/.trae/skills/` | `.trae/skills/` |
| **Trae（中文版）** | ✅ | `~/.trae-cn/skills/` | `.trae/skills/` |
| **CodeBuddy（腾讯）** | ✅ | `~/.codebuddy/skills/` | `.codebuddy/skills/` |
| **Qoder（阿里）IDE** | ✅ | `~/.qoder/skills/` | `.qoder/skills/` |
| **Qoder CN CLI** | ✅（项目级） | 文档未列出 | `.qoder/skills/` |
| **通义灵码 / Lingma（Qoder CN IDE）** | ✅ | `~/.lingma/skills/` | `.lingma/skills/` |
| **Kimi Code CLI（月之暗面）** | ✅ | `~/.kimi-code/skills/` 或 `~/.agents/skills/` | `.kimi-code/skills/` 或 `.agents/skills/` |
| **Qwen Code（通义千问）** | ✅ | `~/.qwen/skills/` 或 `~/.agents/skills/` | `.qwen/skills/` 或 `.agents/skills/` |
| **DeepSeek Harness（`dsh`）** | ✅ | `~/.agents/skills/`（见下方说明 ¹） | `.dsh/skills/` 或 `.agents/skills/` |
| **智谱 CodeGeeX** | ❓ 官方文档里没找到 | — | 用下面的“规则文件版” |
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

### 工具不支持 skill？用规则文件版

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

规则文件每次对话都会整段塞进上下文，所以那一版故意写短。想要含意对照表、冲突优先级和例子，用完整的 `SKILL.md`。

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

- skill 能让助手更守规矩，不能保证。助手有时仍会漏。发现了，就把那条回复发给它，说“这里违反了哪条准则”，它通常会改。
- 格莱斯的原话只有四条准则和合作原则本身。**“质优先于量”等冲突优先级，是我为 AI 助手这个场景定的，不是格莱斯的主张。** 来源和这一区分，见 [`references/SOURCES.md`](skills/grice-cooperative-principle/references/SOURCES.md)。
- 这个 skill 是中文写的，助手会按你对话用的语言回复。需要英文版的话，欢迎 PR。
- 创作、闲聊类的回复，量和方式可以放宽，skill 里写明了。

## 许可

[MIT](LICENSE)。随便用，随便改，随便装进你的团队。

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

# grice-skill · Make your AI assistant talk like a reliable colleague

[简体中文](#grice-skill--让-ai-助手说话像靠谱的同事) | **English**

A skill about *how* an assistant talks, built on H. P. Grice's Cooperative Principle: **say enough, say what's true, answer the question, be clear.**
Once installed, your assistant stops saying "should be fine", "some tests passed" or "handled" and gives you something you can act on.

**Without it:**

> Deployed. New version is live and monitoring looks normal.

**With it:**

> The new version is deployed, but the "warm cache" step timed out (`warmup.sh`, exit code 124), so the cache is cold and the first requests will be slow. I only watched monitoring for 2 minutes and saw no error-rate increase. Want me to re-run the warm-up?

It changes nothing about your code, commands or data. It only shapes how the assistant replies.

## The four maxims

| Maxim | In one line | What the assistant does |
|---|---|---|
| **Quantity** | Enough, not more | Answer first; include the command/path/number you need next; cut restating and closing summaries |
| **Quality** | Only what's true | No evidence from this turn → "not verified". Don't know → say so, don't guess |
| **Relation** | Answer the question | The asked question, not a neighbouring one; correct a wrong premise in the first sentence |
| **Manner** | Be clear | Unambiguous references, times with a timezone, no weak wording that reads as something stronger |

The skill also has an implicature table ("no issues found" is heard as "everything was checked"), an order of priority for clashes (quality > quantity), a handoff template for passing work to another agent, an 8-point pre-send check, and 8 before/after examples. See [`SKILL.md`](skills/grice-cooperative-principle/SKILL.md) (about 220 lines, written in Chinese; the assistant replies in the language you use).

## Install

### Easiest: ask your assistant to install it

In Claude Code, Codex, Cursor, Trae, CodeBuddy, Qoder, Qwen Code, Kimi Code CLI or similar, say:

```text
Install this skill for me: https://github.com/ZHUCH-520/grice-skill/tree/main/skills/grice-cooperative-principle
```

Then start a new conversation and ask "which skills do you have?". If `grice-cooperative-principle` is listed, you're done.

### Command line

```bash
npx skills add ZHUCH-520/grice-skill
```

This uses the generic [vercel-labs/skills](https://github.com/vercel-labs/skills) installer, which lists support for Claude Code, Codex, Cursor, Gemini CLI, CodeBuddy, Lingma, Qoder, Qwen Code, Trae, Kimi Code CLI and more. For Gemini CLI alone:

```bash
gemini skills install https://github.com/ZHUCH-520/grice-skill.git --path skills/grice-cooperative-principle
```

### Manual: copy the folder

Copy `skills/grice-cooperative-principle/` into the skills directory of your tool. The directories in the table above (Chinese section) come from each tool's official documentation, checked on 2026-10-31. Short version: Claude Code `~/.claude/skills/`, Codex / Cursor / Gemini CLI / Qwen Code / Kimi Code CLI `~/.agents/skills/` (also read by several others), Trae `~/.trae/skills/` (China edition `~/.trae-cn/skills/`), CodeBuddy `~/.codebuddy/skills/`, Qoder `~/.qoder/skills/`, Lingma `~/.lingma/skills/`, Qwen Code `~/.qwen/skills/`, DeepSeek Harness `.dsh/skills/` or `.agents/skills/` in the project. I checked the documented paths; I did not run every tool end to end.

### No skill support? Use the rules snippet

Paste the block in [`snippets/rules-snippet.md`](snippets/rules-snippet.md) (about 10 lines, Chinese and English) into `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `QWEN.md`, `CODEBUDDY.md`, or the tool's rules directory (`.cursor/rules/`, `.trae/rules/`, `.qoder/rules/`, `.lingma/rules/`).

### Can't reach GitHub?

Copy the text of `SKILL.md` into a folder named `grice-cooperative-principle` in the right directory; or download the ZIP from a machine that can reach GitHub. A Gitee mirror is planned but not set up yet.

## Notes

- A skill makes an assistant more disciplined; it doesn't guarantee it. If a reply slips, quote it back and name the maxim it broke.
- Grice himself gave the Cooperative Principle and four maxims. The conflict priority "quality beats quantity" is my own rule for AI assistants, not Grice's. See [`references/SOURCES.md`](skills/grice-cooperative-principle/references/SOURCES.md).
- Creative writing and chit-chat relax Quantity and Manner; the skill says so.

## License

[MIT](LICENSE).
