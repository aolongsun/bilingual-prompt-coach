# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

Practice a language through real work. This explicitly activated Codex Skill gives concise language feedback before completing your request and adds support in your primary language only where it helps.

The defaults are Chinese support and clear B2–C1 American English practice. You can choose both languages, the target-language variety and level, feedback depth, and bilingual balance.

The links above change the documentation language only. They do not change your practice configuration; state your language preferences in the conversation.

![English example showing corrections in bold](docs/output-example.png)

*The image shows an English output example. Only changes in the minimal correction are bold.*

![English decision map for coaching behavior](docs/decision-map.jpg)

*This decision map is in English and illustrates when coaching appears.*

## Overview

Use your everyday requests to study, research, code, or handle other tasks while learning from a small amount of reusable language feedback. The task answer still follows the feedback.

- English or other target-language prompts receive a minimal correction and a natural rewrite when useful.
- Prompts entirely in your primary language receive one natural version in the target language.
- Mixed-language prompts are converted into the target language while preserving meaning.
- Clear, natural prompts get a brief note instead of redundant rewrites.
- Difficult passages can receive short primary-language explanations directly below the relevant passage. Ordinary answers are not translated paragraph by paragraph.

## Installation

Ask Codex to use its built-in installer:

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

Alternatively, clone the repository into your personal skills directory:

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

Restart Codex if the skill does not appear immediately.

## Usage

Explicitly invoke the skill with a substantive request:

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

Coaching stays active for the current task without repeated invocation. A new task starts with practice mode off. Any of these turns it off:

```text
off
OFF!
stop coaching
```

You can also ask to stop in your own language. An unrelated instruction such as `turn the server off` does not deactivate coaching.

## Choose your languages and feedback

Your primary/support language and target/practice language are separate settings. Set both naturally, including when activating the skill:

```text
$bilingual-prompt-coach My primary language is Japanese, and I want to practice English.
My primary language is Chinese, and I want to practice Japanese.
Use British English at B1 level.
English only.
More Chinese, please.
No correction notes.
No highlighting.
Correct the full text.
```

The latest explicit choice wins within the current task. Without an override, the defaults remain Chinese support and B2–C1 American English. Choosing a different README does not set either language.

An explicitly requested deliverable language takes priority for the task answer. For example, `Answer this question in Chinese` produces a Chinese task answer while retaining any applicable language practice block. Explanatory `Why` notes normally use the target language, with primary-language help only when needed.

## Example

Input:

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

Example response:

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

Only inserted or replaced text in `Minimal correction` is bold. `Natural phrasing` and the task answer have no change highlighting. Ordinary deletions are removed cleanly; there is no default strikethrough, HTML coloring, or diff markup. You can request plain corrections without highlighting.

For a prompt entirely in your primary language, the block uses `Natural version` instead of `Minimal correction` and `Natural phrasing`.

## Boundaries

- Coaching appears at most once, at the beginning of the final answer, never in progress updates or intermediate planning. Pure JSON, code, or other required output formats take priority.
- Greetings, acknowledgements, option selections, attachments without substantive prose, and brief coordination such as `continue` or `implement the plan` do not need a coaching block.
- Quotations, pasted sources, code, commands, logs, filenames, and data are excluded unless you ask to edit them.
- When proofreading, rewriting, or translation is itself the requested deliverable, no duplicate coaching block is added unless requested.
- For prompts longer than 150 words, up to three useful excerpts are selected instead of repeating the full prompt twice. Request a full edit to override this.
- Rewrites preserve meaning, tone, claims, and specificity. They do not add ideas or make the request stronger or weaker.

This is an instruction-only skill with no runtime scripts, external-tool dependencies, or hidden cross-task memory. Practice mode relies on the current conversation. [SKILL.md](SKILL.md) contains the single English instruction set; translated READMEs explain the same skill rather than defining separate versions. The [behavior checklist](tests/behavior-cases.md) documents validation scenarios.

## License

[MIT](LICENSE)
