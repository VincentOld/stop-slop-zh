# Stop AI Slop · 中文版

<!-- yarkr:badges:start -->
[![Indexed on Yarkr](https://api.yarkr.com/functions/v1/api/api/v1/badges/repos/VincentOld/stop-slop-zh/version.svg)](https://yarkr.com/arks/vincentold/stop-slop-zh)
<!-- yarkr:badges:end -->

让 AI 写出来的中文不再像 AI 写的。

这是一套提示词 Skill，给 Claude / GPT / Gemini / 文心 / 通义 / DeepSeek 等模型用，识别并消除中文 AI 写作的典型痕迹：套话、排比三件套、名词化动词、抽象主语、金句收尾、总分总八股。

灵感来自 [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) 英文项目，但**不是翻译**——中文 AI 味跟英文 AI 味的指纹完全不一样，整套规则、词表、句式、评分都是为中文重做的。

---

## 这套规则解决什么

你大概见过这样的中文：

> 在当今 AI 蓬勃发展的时代，我们正面临前所未有的机遇与挑战。AI 不仅是一种工具，更是一种思维方式，是推动社会进步的重要力量。让我们以更开放的姿态拥抱变化，共创美好未来。

每一句都对，但你一眼能看出是 AI 写的。本 Skill 要解决的就是这种"每一句都对、但合在一起就是 AI"的问题。

## 项目结构

```
.
├── SKILL.md              核心：8 条改写规则 + 5 维评分 + 工作流
├── README.md             本文件
└── references/
    ├── phrases.md        12 类禁用词汇黑名单（约 200 条）
    ├── structures.md     15 类句式套路（含三件套 / 名词化 / 抽象主语等）
    └── examples.md       4 个场景 7 组 Before/After 改写示例
```

## 怎么用

### 方式 1：Claude Code（推荐）

把整个目录放到 Claude Code 能扫到的 skills 路径下，或直接 `cd` 到本目录后，第一句对话告诉 Claude：

> 请按 SKILL.md 的规则改写下面这段中文。改完后给五维打分。

Claude 会自动读取 SKILL.md 和 references。

### 方式 2：Claude Projects / ChatGPT Projects

把 `SKILL.md` 和 `references/*.md` 全部上传到 Project 的知识库。然后在系统提示或第一句对话里写：

> 你扮演中文 AI 味消除助手。所有改写任务都要遵循 SKILL.md 中的 8 条规则与 5 维评分。模糊时优先查 references/phrases.md 和 references/structures.md。

### 方式 3：单次 API 调用 / Cherry Studio / 其他客户端

把 `SKILL.md` 全文塞进系统提示。`references/*.md` 可以按需放入，或拼成一个长 prompt。

最小可用 prompt 模板：

```
你的任务是消除中文 AI 写作痕迹。严格按以下规则操作：

[此处粘贴 SKILL.md 全文]

每次改写后，按五维评分（直/实/变/散/真，每维 1-10）打分，
低于 35/50 重写直到达标。

用户输入：[待改写文本]
```

### 方式 4：作为人工校稿清单

不接 LLM 也能用。`SKILL.md` 第四节"交付前清单"是 9 条人工查的项目，写完文章对着清单走一遍。

## 用法建议

- **不要边写边查**。先把想说的写完，再用本 Skill 改写。边写边查会丢失思路。
- **从 phrases.md 第 1 / 5 / 7 / 10 类开始**：这四类（开场套话 / 程度副词 / 鸡汤收尾 / 价值判断饱和）命中率最高，最快见效。
- **重灾区是三件套排比**。改写时优先全文搜「，是」「，更是」「既要」「不仅」，命中的位置看一下要不要拆。
- **35/50 是底线，不是目标**。要让文本读起来像人写的，至少 42+。
- **作者的具体经历是最强武器**。AI 写不出来的不是技巧，是你知道而 AI 不知道的细节。

## 边界与坦诚

这套规则不是万能的：

- **公文 / 党政文稿**：里面的"总分总"和价值判断是规范，不是 AI 味。本 Skill 在这类文本上要保守使用。
- **法律 / 合同**：精确性优先，名词化和长定语是必要的。
- **学术论文**：被动语态和抽象主语在学术写作里是常态，不必强拆。
- **小红书 / 抖音文案**：本身就是高度套路化的格式，本 Skill 的目标变成"换一种套路"而不是去套路化。

详见 SKILL.md 第五节"什么时候不该用本 Skill"。

## 持续更新

中文 AI 文本的指纹在变。模型更新一轮，套话就换一批。

新词收录标准：在三篇不同来源（不同模型 / 不同 prompt / 不同作者）的 AI 输出里都出现过，才进黑名单。避免误伤个人风格。

欢迎反馈遇到的新型 AI 套话，特别是：
- 某个模型 / 某个版本的特有指纹
- 某个垂直领域（医美、母婴、金融）的套话
- 你试过本 Skill 但发现没盖到的场景

## 致谢

- [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop)：英文版项目，提供了三层架构（词汇黑名单 / 句式模式 / 评分量规）的设计思路
- Anthropic Skill 规范：本项目按 Claude Skill 标准组织文件结构

## 协议

MIT

<!-- yarkr:install:start -->
## Install with Yarkr

This repo is indexed on [Yarkr](https://yarkr.com/arks/vincentold/stop-slop-zh) as the ark [vincentold/stop-slop-zh](https://yarkr.com/arks/vincentold/stop-slop-zh), so its skills install into Claude Code, Codex, Cursor and other agent harnesses with one command.

### CLI

Install the whole ark, which Yarkr keeps equal to this repo:

```bash
npx yarkr-cli sync vincentold/stop-slop-zh
```

Or add individual skills:

```bash
npx yarkr-cli add skill:vincentold/stop-slop-zh/stop-ai-slop-zh
```

No Node.js? `curl -fsSL https://yarkr.com/install.sh | sh` (macOS, Linux) or `irm https://yarkr.com/install.ps1 | iex` (Windows PowerShell) installs `yarkr` as a standalone binary; then type `yarkr` in place of `npx yarkr-cli`.

### MCP

Connect your agent to the ark over MCP:

```bash
npx yarkr-cli mcp add vincentold/stop-slop-zh
```

Or point any MCP client at `https://api.yarkr.com/functions/v1/api/mcp/o/vincentold/stop-slop-zh`.
<!-- yarkr:install:end -->
