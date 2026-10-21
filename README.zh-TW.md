# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

在完成實際任務的同時練習語言。這個需要明確啟用的 Codex Skill 會先提供簡潔的語言回饋，再完成你的請求，並且只在確實有幫助時補充母語／輔助語言的說明。

預設使用中文輔助，練習清晰的 B2–C1 美式英語。你可以分別選擇兩種語言，並調整練習語言的變體、程度、回饋深度與雙語比例。

上方連結只切換文件的閱讀語言，不會自動改變練習設定。請在對話中明確說明你的語言偏好。

![英文輸出範例：修改處以粗體顯示](docs/output-example.png)

*圖片呈現的是英文輸出範例。只有最小修改版中變更的文字使用粗體。*

![英文語言回饋判斷流程圖](docs/decision-map.jpg)

*這張流程圖使用英文，說明何時提供語言回饋。*

## 簡介

照常提出學習、研究、程式開發或日常工作中的請求，同時從少量可重複運用的語言回饋中學習。語言回饋之後仍會完整回答原始問題。

- 對英文或其他練習語言的提示，在有幫助時提供最小修改版與自然表達版。
- 對完全使用母語／輔助語言的提示，提供一個自然的練習語言版本。
- 對混合語言的提示，在保留原意的前提下轉換為練習語言。
- 對已經清晰自然的表達，只給簡短提示，不重複改寫。
- 對難懂的段落，可在其下方緊接簡短的輔助語言說明，不逐段重複翻譯一般回答。

## 安裝

請 Codex 使用內建安裝工具：

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

也可以將儲存庫複製到個人的 skills 目錄：

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

如果 skill 沒有立即出現，請重新啟動 Codex。

## 使用方式

在包含實質請求的訊息中明確呼叫：

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

啟用後，語言回饋會在目前任務中持續生效，無須重複呼叫。新任務預設關閉練習模式。以下表達都能關閉：

```text
off
OFF!
stop coaching
關閉語言練習。
```

也可以用自己的語言要求停止。`turn the server off` 這類無關指令不會關閉語言回饋。

## 設定語言與回饋

母語／輔助語言與目標／練習語言是兩個獨立設定，可以用自然語言分別指定，也可以在啟用時一起設定：

```text
$bilingual-prompt-coach 我的母語是日語，我想練習英語。
我的母語是中文，我想練習日語。
使用 B1 程度的英式英語。
只用英語。
請多用一些中文。
不需要糾錯說明。
不需要醒目標示。
請修改全文。
```

目前任務內，以最近一次明確設定為準。未另行設定時，仍預設中文輔助、B2–C1 美式英語練習。切換 README 不會設定任何一種語言。

如果明確指定交付語言，任務正文優先使用該語言。例如「請用中文回答這個問題」會得到中文任務答案，同時仍可保留適用的語言練習區塊。`Why` 通常使用練習語言，只有必要時才補充輔助語言說明。

## 範例

輸入：

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

回答範例（保留英文，方便觀察修正）：

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

`Minimal correction` 只對插入或替換的文字加粗；`Natural phrasing` 與任務正文不標示變更。刪除的內容直接移除，預設不使用刪除線、HTML 顏色或 diff 標記。你也可以要求不加醒目標示，只顯示一般修正結果。

對完全使用母語／輔助語言的提示，區塊會用 `Natural version` 取代 `Minimal correction` 與 `Natural phrasing`。

## 行為界線

- 每輪最多一次語言回饋，放在最終回答開頭，不出現在進度更新或中間規劃中。要求純 JSON、程式碼等格式時，優先遵守交付格式。
- 問候、確認、選項選擇、沒有實質文字的附件，以及「繼續」「實施計畫」等簡短協調訊息，不需要語言回饋區塊。
- 除非要求編輯，否則不修改引文、貼上的資料、程式碼、指令、記錄、檔名與資料。
- 當校對、改寫或翻譯本身就是交付任務時，除非另有要求，否則不重複添加語言回饋區塊。
- 超過 150 詞的提示預設選擇最多三個有學習價值的片段，不完整重複兩遍；可以要求全文修改。
- 改寫保留含義、語氣、主張與具體程度，不添加想法，也不強化或弱化請求。

這是一個純指令型 skill，沒有執行階段腳本、外部工具相依性或跨任務隱藏記憶。練習模式依賴目前對話。[SKILL.md](SKILL.md) 是唯一的英文執行規則；各語言 README 是同一 skill 的說明，而非獨立版本。[行為檢查表](tests/behavior-cases.md) 記錄了驗證情境。

## 授權條款

[MIT](LICENSE)
