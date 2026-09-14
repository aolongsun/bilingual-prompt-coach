# Behavior Test Matrix

Use this checklist for manual forward-testing. Judge observable behavior and preserved
meaning rather than exact wording.

| ID | Scenario | Example input | Expected behavior |
| --- | --- | --- | --- |
| A1 | Explicit activation with prose | `$bilingual-prompt-coach I have read Dreamer yesterday and I have some questions.` | Coaching appears once at the beginning of the final answer, followed by the task answer. |
| A2 | Activation only | `Enable practice mode for this task.` | Brief confirmation; no coaching block. |
| A3 | Task persistence | After A1: `Does the actor also choose imagined actions?` | Coaching continues without another invocation. |
| A4 | Bare deactivation | `off` | Brief acknowledgement; no coaching. Later turns remain uncoached. |
| A5 | Punctuated deactivation | `OFF!` | Same as A4. |
| A6 | Natural-language deactivation | `I need to stop using this skill.` / `关闭英语练习。` | Practice mode stops; the request itself is not coached. |
| A7 | False-positive protection | While active: `Turn the server off after the tests pass.` | Treat as a task instruction, not skill deactivation. |
| E1 | Brief coordination | `implement the plan` / `yes` / `continue` | No coaching block. |
| E2 | Attachment only | An image with no substantive user prose | No coaching block. |
| E3 | Already natural | `Could you explain how Dreamer's actor learns from imagined trajectories?` | One `Language note: Already natural.`; no redundant rewrites. |
| E4 | Proofreading task | `Rewrite this paragraph naturally: ...` | The requested rewrite is the language deliverable; no duplicate coaching block. |
| O1 | Commentary separation | A tool-using task with progress updates | No corrections in commentary; at most one coaching block in the final answer. |
| O2 | Plan Mode | A task requiring exploration before a plan | No coaching in deliberation or progress; eligible feedback appears at most once in the final response. |
| O3 | Pure output | `Return only this JSON schema ...` | Omit coaching rather than violate the pure-format contract. |
| I1 | Chinese-only prompt | `请解释 Dreamer 中 actor 和 world model 的关系。` | One `Natural version`; no `Minimal correction`; no more than two notes. |
| I2 | Mixed-language prompt | `Dreamer 的 actor 是不是也会在 imagination 中选择 actions?` | Both versions convert the Chinese portions naturally and preserve meaning. |
| I3 | Long prompt | More than 150 words with several problems | Correct up to three high-value excerpts; do not repeat the full prompt twice. |
| I4 | Excluded material | Prose plus quoted text, code, filenames, logs, and data | Coach only the user's surrounding prose; excluded material remains unchanged. |
| H1 | Replacement highlight | `The actor take actions.` | `Minimal correction` contains `The actor **takes** actions.`; only the replacement is bold. |
| H2 | Insertion highlight | `I read paper.` | `Minimal correction` contains `I read **a** paper.`; only the insertion is bold. |
| H3 | Adjacent changes | A phrase requiring several adjacent corrected words | Use one readable bold span instead of separate bold markers around every word. |
| H4 | Punctuation highlight | `However I disagree.` | `Minimal correction` begins `**However,** I disagree.` so the affected phrase and punctuation form one readable span. |
| H5 | Pure deletion | `Please return back.` | Produce the clean correction `Please return.` without strikethrough, HTML, or a diff block; explain the deletion in `Why` only if useful. |
| H6 | Mixed-language highlight | `The actor 会选择 imagined actions.` | In `Minimal correction`, the translated target-language span is bold; unchanged English is not. |
| H7 | Highlighting scope and override | `No highlighting, please. I have read Dreamer yesterday.` | Correct the prompt without change highlighting. By default, `Natural phrasing` and the task answer also remain unmarked. |
| B1 | Difficult technical answer | Ask for a dense mathematical explanation | Add Chinese only where comprehension risk is high, directly below the related English passage. |
| B2 | English-only override | `English only.` plus a substantive request | No Chinese support anywhere in the response. |
| B3 | Deliverable-language override | `Answer the technical question in Chinese.` | The task answer is Chinese; applicable language practice may still precede it. |
| B4 | Full-edit override | A prompt over 150 words plus `Correct the full text.` | Provide the requested complete correction instead of excerpt selection. |

## Release checklist

- [ ] `SKILL.md` passes the bundled `quick_validate.py` validator.
- [ ] `agents/openai.yaml` parses and keeps `allow_implicit_invocation: false`.
- [ ] The Skill name, directory name, README examples, and default prompt agree.
- [ ] All cases above were reviewed against the current instructions.
- [ ] Replacement, insertion, punctuation, deletion, mixed-language, and no-highlight cases render as specified without HTML/CSS color tags.
- [ ] `docs/output-example.png` and `docs/decision-map.jpg` are legible in a rendered README and contain no private data.
- [ ] Repository files contain no absolute local paths, secrets, placeholders, or private screenshots.
- [ ] The repository contains only the eight documented release files.
- [ ] Git status is clean, tag `v0.1.0` remains unchanged, and tag `v0.1.1` points to the highlight release.
