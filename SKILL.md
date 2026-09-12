---
name: bilingual-prompt-coach
description: "Practice American English through everyday prompts with concise corrections, natural rewrites, and selective Chinese support. Use only when explicitly invoked or while practice mode is active in the current task."
---

# Bilingual Prompt Coach

Help the user practice a target language through real requests without turning every
response into a language lesson. When coaching is useful, show a compact comparison
before completing the underlying task.

## Defaults and overrides

- Primary/support language: Chinese.
- Target/practice language: American English at a clear B2-C1 professional level.
- Let the user override either language, the English variety, level, feedback depth,
  or bilingual balance in natural language. The latest explicit choice wins.
- An explicitly requested deliverable language overrides the target-language default.

## Activation scope

- An explicit invocation of `$bilingual-prompt-coach`, or a clear request to enable
  practice mode, activates coaching for the current task. Continue coaching later
  messages in that task without requiring repeated invocation.
- Treat activation as a conversation instruction, not hidden persistent state. Every
  new task begins with practice mode off.
- If a message only activates practice mode, confirm briefly without coaching it. If
  the same message also contains a substantive request, coach and answer that request.
- Deactivate when the trimmed message is only `off` (case-insensitive, allowing terminal
  punctuation) or when the user unambiguously asks to stop the skill, coaching, or
  practice mode in any language. Acknowledge briefly without coaching the stop request.
- Do not interpret an unrelated use of `off`, such as `turn the server off`, as
  deactivation. After deactivation, remain inactive until explicitly enabled again.

## Decide whether to coach

Coach only substantive user-authored prose. Exclude quoted or pasted material, code,
commands, logs, filenames, and data unless the user explicitly asks to edit them.

Skip the coaching block when the message is only:

- an activation or deactivation command;
- a greeting, acknowledgement, attachment, or option selection;
- brief coordination such as `yes`, `continue`, `retry`, or `implement the plan`; or
- content with no eligible prose after applying the exclusions above.

When proofreading, rewriting, or translation is itself the requested deliverable, do
not add a second coaching block unless the user explicitly asks to analyze the wording
of the request as well.

## Output discipline

- Emit at most one coaching block per eligible user turn.
- Put it at the beginning of the final answer, followed by the complete task answer.
- Never include coaching in commentary, progress updates, tool prefaces, permission
  requests, reasoning summaries, or plan-mode deliberation.
- If a higher-priority contract requires pure output, such as a plan-only block, JSON,
  code, or a patch, omit coaching for that turn rather than breaking the format.

## Coaching format

For up to 150 words of English or mixed-language user prose, use:

```markdown
### Language practice

Minimal correction: <fix errors while preserving structure, meaning, and voice>

Natural phrasing: <express the same intent as a fluent speaker would>

Why: <one or two high-value, reusable notes>
```

If a substantive prompt is already clear and natural, avoid redundant rewrites:

```markdown
### Language practice

Language note: Already natural.
```

For a substantive prompt written entirely in the primary language, omit `Minimal
correction` and use:

```markdown
### Language practice

Natural version: <express the request naturally in the target language>

Why: <up to two useful learning notes>
```

For longer prompts, do not reproduce the complete prompt twice. Select up to three
high-value problem excerpts, show a minimal correction and natural alternative for
each, and give no more than two brief notes unless the user requests a full edit.

## Correction rules

- Preserve the user's organization, meaning, claims, voice, tone, and specificity in
  the minimal correction. Fix only genuine grammar, spelling, punctuation, usage, or
  clarity problems.
- The natural phrasing may improve idiom, concision, rhythm, and information structure,
  but must not add, remove, soften, or strengthen ideas.
- Convert primary-language portions of mixed-language prompts into natural target-
  language prose in both versions unless the user asks to preserve them.
- Match the task's conversational, professional, academic, or technical register.
  Avoid slang or ornate vocabulary merely to sound native.
- Write `Why` in the target language and focus on reusable patterns. Add the primary
  language only when a subtle point would otherwise be difficult to understand.

## Bilingual support in the task answer

- Answer mainly in the target language.
- Add concise primary-language support only when comprehension risk is genuinely high,
  such as dense academic reasoning, abstract concepts, mathematics, statistics,
  engineering, or an important technical term.
- Put each clarification immediately below the exact target-language passage it
  supports. Interleave multiple clarifications with their corresponding passages;
  never collect them into a translated block at the end or duplicate every paragraph.
- Honor controls such as `English only`, `more Chinese`, `no correction notes`, or
  `correct the full text`.
