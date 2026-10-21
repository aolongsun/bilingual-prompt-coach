# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

実際の作業を通じて言語を練習するための Codex Skill です。明示的に有効にすると、依頼に答える前に簡潔な言語フィードバックを示し、役立つ場合にだけ母語・補助言語で説明を添えます。

初期設定は中国語による補助と、明快な B2–C1 レベルのアメリカ英語の練習です。両方の言語に加え、練習言語の地域変種、レベル、フィードバックの詳しさ、二言語の割合を変更できます。

上のリンクで変わるのはドキュメントの表示言語だけです。練習設定は自動では変わりません。希望する言語は会話の中で指定してください。

![修正箇所を太字にした英語の出力例](docs/output-example.png)

*画像は英語の出力例です。最小限の修正案で変更した部分だけが太字になります。*

![言語フィードバックの判断を示す英語のフロー図](docs/decision-map.jpg)

*この図は英語で、フィードバックを表示する条件を説明しています。*

## 概要

学習、研究、プログラミング、日常の仕事について普段どおりに質問しながら、応用できる短い言語フィードバックで学べます。その後には、元の依頼への回答が続きます。

- 英語を含む練習言語のプロンプトには、役立つ場合に最小限の修正案と自然な表現を提示します。
- 全文が母語・補助言語の場合は、練習言語で自然に表した文を一つ提示します。
- 複数言語が混ざったプロンプトは、意味を保ったまま練習言語にまとめます。
- すでに明快で自然な文には、重複した書き換えの代わりに短いコメントを添えます。
- 難しい箇所には、その直下に短い補助言語の説明を添えられます。通常の回答を段落ごとに重複翻訳することはありません。

## インストール

Codex に内蔵インストーラーの利用を依頼します。

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

または、個人用の skills ディレクトリにリポジトリをクローンします。

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

すぐに表示されない場合は Codex を再起動してください。

## 使い方

具体的な依頼を含むメッセージで明示的に呼び出します。

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

有効化後は、同じタスク内で毎回呼び出す必要はありません。新しいタスクでは練習モードは無効に戻ります。次のどの表現でも終了できます。

```text
off
OFF!
stop coaching
言語練習を終了してください。
```

自分の言語で終了を依頼することもできます。`turn the server off` のような無関係な指示では、言語フィードバックは無効になりません。

## 言語とフィードバックの設定

母語・補助言語と、目標・練習言語は別々の設定です。自然な言葉で指定でき、有効化と同時に設定することもできます。

```text
$bilingual-prompt-coach 母語は日本語で、英語を練習したいです。
母語は中国語で、日本語を練習したいです。
B1 レベルのイギリス英語を使ってください。
英語だけで答えてください。
中国語の説明を増やしてください。
修正についての説明は不要です。
変更箇所を強調しないでください。
全文を修正してください。
```

現在のタスクでは、最後に明示した設定が優先されます。指定がなければ、中国語による補助と B2–C1 のアメリカ英語が初期設定です。README の切り替えは、どちらの言語の設定も変更しません。

成果物の言語を明示した場合は、タスクの回答にその言語を使います。たとえば「この質問には中国語で答えてください」と指定すると、必要に応じて言語練習の欄を残しつつ、回答本文は中国語になります。`Why` の説明は通常、練習言語で書き、必要な場合だけ補助言語を添えます。

## 例

入力：

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

回答例（修正を確認できるよう英語のまま示します）：

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

`Minimal correction` では、挿入・置換した文字だけを太字にします。`Natural phrasing` と回答本文には変更箇所の強調を付けません。削除は文から取り除き、標準では取り消し線、HTML による色付け、diff 表記を使いません。強調のない修正を依頼することもできます。

全文が母語・補助言語の場合は、`Minimal correction` と `Natural phrasing` の代わりに `Natural version` を使います。

## 動作の範囲

- 言語フィードバックは各ターンの最終回答の冒頭に最大一回表示します。進捗報告や途中の計画には表示しません。JSON のみ、コードのみなどの出力指定を優先します。
- 挨拶、了承、選択肢への回答、実質的な文章のない添付ファイル、「続けて」「計画を実行して」などの短い連絡には表示しません。
- 引用、貼り付けた資料、コード、コマンド、ログ、ファイル名、データは、編集を依頼されない限り対象外です。
- 校正、書き換え、翻訳そのものが依頼内容なら、別途求められない限り二重のフィードバック欄は付けません。
- 150 語を超えるプロンプトでは、全文を二回繰り返さず、学習に役立つ箇所を最大三つ選びます。全文修正を指定すれば、この制限を変更できます。
- 書き換えでは意味、語調、主張、具体性を保ちます。考えを付け加えたり、依頼を強めたり弱めたりしません。

この skill は指示のみで構成され、実行用スクリプト、外部ツールへの依存、タスクをまたぐ隠れた記憶はありません。練習モードは現在の会話に基づきます。実行ルールは英語の [SKILL.md](SKILL.md) に一本化されており、翻訳版 README は同じ skill の説明です。[動作チェックリスト](tests/behavior-cases.md) に検証シナリオを記載しています。

## ライセンス

[MIT](LICENSE)
