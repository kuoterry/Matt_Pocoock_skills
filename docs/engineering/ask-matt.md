Quickstart:

```bash
npx skills add mattpocock/skills --skill=ask-matt
```

```bash
npx skills update ask-matt
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt)

## What it does

`ask-matt` 是這個 repo 裡所有 skill 的 router。你描述你目前的情況;它告訴你哪個 skill 或流程適合,以及該用什麼順序執行。

它**自己不做任何實際工作**。它不會 grill、不會寫 spec、也不會修任何東西 —— 它只負責定向。它的存在,首先是為了那些 **user-invoked** 的 skill:沒有東西會替你觸發它們,所以*你*得記得它們的存在,而 `ask-matt` 就是你可以把這份記憶外包出去的地方。它也會指向你會直接叫名字用的 model-invoked skill —— `/tdd`、`/diagnosing-bugs`、`/prototype`、`/code-review`,以及兩個詞彙參考 `/domain-modeling` 與 `/codebase-design`。它回答「該用哪一個、什麼時候用」,然後把你交給真正做事的那個 skill。

## When to reach for it

你打 `/ask-matt` 來觸發它 —— agent 不會自己去找它。

每當你不確定某個情況該用哪個 skill 或流程時,就用它:你有個點子但不知道從哪開始、手上一堆 bug 回報不知道是不是該用 `/triage`、或是兩個看起來很像的 skill 分不清楚差在哪。如果你已經知道要用哪個 skill,就跳過 router,直接觸發它。

## 不只是 skill,還有 flow

`ask-matt` 給你的思考工具是 **flow** —— 一條*穿過*一組 skill 的路徑,而不是單一一個 skill。多數工作沿著一條**主流程**走(從點子到出貨:grill → spec → tickets → implement → review),有兩條**匝道**併進來(給進來的 bug 與需求走的 triage 車道;產生點子的 codebase 健康度車道),其餘的都是可以**單獨拿來用**的獨立工具。你問一個問題,就會被安放到對的 flow、對的那一步 —— 而不只是拿到一個工具。

## Where it fits

`ask-matt` 是 **router** —— 蓋在整組 skill 上面的獨立地圖。它是每一頁其他 docs 頁都會用 [ask-matt](https://aihero.dev/skills-ask-matt) 連回去的那個節點,所以它從不身處*在*某條鏈裡面;它是*指向*每一條鏈的那個點。從這裡出發,你最常會落在主流程開頭的 [grill-with-docs](https://aihero.dev/skills-grill-with-docs),或是給非自己開的工作走的匝道 [triage](https://aihero.dev/skills-triage)。當連 router 自己畫的圖都過時了,它的 [Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/ask-matt) 就是最準的那份地圖。
