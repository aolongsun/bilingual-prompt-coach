# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

在完成真实任务的同时练习语言。这个需要显式启用的 Codex Skill 会先提供简洁的语言反馈，再完成你的请求，并且只在确实有帮助时补充母语言／支持语言的解释。

默认使用中文辅助，练习清晰的 B2–C1 美式英语。你可以分别选择两种语言，并调整练习语言的变体、水平、反馈深度和双语比例。

上方链接只切换文档的阅读语言，不会自动改变练习配置。请在对话中明确说明你的语言偏好。

![英文输出示例：修改处以粗体显示](docs/output-example.png)

*图片展示的是英文输出示例。只有最小修改版中改动的文字使用粗体。*

![英文语言反馈判断流程图](docs/decision-map.jpg)

*这张流程图使用英文，说明何时提供语言反馈。*

## 简介

照常提出学习、研究、编程或日常工作中的请求，同时从少量可复用的语言反馈中学习。语言反馈之后仍会完整回答原始问题。

- 对英文或其他练习语言的 prompt，在有帮助时提供最小修改版和自然表达版。
- 对完全使用母语言／支持语言的 prompt，提供一个自然的练习语言版本。
- 对混合语言的 prompt，在保留原意的前提下转换为练习语言。
- 对已经清晰自然的表达，只给简短提示，不重复改写。
- 对难懂的段落，可在其下方紧接简短的支持语言解释，不逐段重复翻译普通回答。

## 安装

请 Codex 使用内置安装器：

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

也可以将仓库克隆到个人 skills 目录：

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

如果 skill 没有立即出现，请重启 Codex。

## 使用方式

在包含实质性请求的消息中显式调用：

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

启用后，语言反馈会在当前任务中持续生效，无须重复调用。新任务默认关闭练习模式。以下表达均可关闭：

```text
off
OFF!
stop coaching
关闭语言练习。
```

也可以用自己的语言要求停止。`turn the server off` 这类无关指令不会关闭语言反馈。

## 设置语言和反馈

母语言／支持语言与目标／练习语言是两个独立设置，可以用自然语言分别指定，也可以在启用时同时设置：

```text
$bilingual-prompt-coach 我的母语言是日语，我想练习英语。
我的母语言是中文，我想练习日语。
使用 B1 水平的英式英语。
只用英语。
请多用一些中文。
不需要纠错说明。
不需要高亮。
请修改全文。
```

当前任务内，以最近一次明确设置为准。未覆盖时，仍默认中文辅助、B2–C1 美式英语练习。切换 README 不会设置任何一种语言。

如果明确指定交付语言，任务正文优先使用该语言。例如“请用中文回答这个问题”会得到中文任务答案，同时仍可保留适用的语言练习区块。`Why` 通常使用练习语言，只有必要时才补充支持语言说明。

## 示例

输入：

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

回答示例（保留英文，便于观察纠错）：

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

`Minimal correction` 只对插入或替换的文字加粗；`Natural phrasing` 和任务正文不标记改动。删除的内容直接移除，默认不使用删除线、HTML 颜色或 diff 标记。你也可以要求不高亮、只显示普通修改结果。

对于完全使用母语言／支持语言的 prompt，区块会用 `Natural version` 代替 `Minimal correction` 和 `Natural phrasing`。

## 行为边界

- 每轮最多一次语言反馈，放在最终回答开头，不出现在进度更新或中间规划中。要求纯 JSON、代码等格式时，优先遵守交付格式。
- 问候、确认、选项选择、无实质性文字的附件，以及“继续”“实施计划”等简短协调消息，不需要语言反馈区块。
- 除非要求编辑，否则不修改引用、粘贴资料、代码、命令、日志、文件名和数据。
- 当校对、改写或翻译本身就是交付任务时，除非另有要求，否则不重复添加语言反馈区块。
- 超过 150 词的 prompt 默认选择最多三个有学习价值的片段，不完整重复两遍；可以要求全文修改。
- 改写保留含义、语气、主张和具体程度，不添加想法，也不强化或弱化请求。

这是一个纯指令型 skill，没有运行时脚本、外部工具依赖或跨任务隐藏记忆。练习模式依赖当前对话。[SKILL.md](SKILL.md) 是唯一的英文执行规则；各语言 README 是同一 skill 的说明，而非独立版本。[行为检查表](tests/behavior-cases.md) 记录了验证场景。

## 许可证

[MIT](LICENSE)
