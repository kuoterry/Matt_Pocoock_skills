Quickstart:

```bash
npx skills add mattpocock/skills --skill=grill-with-docs
```

```bash
npx skills update grill-with-docs
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs)

## What it does

`grill-with-docs` 針對一個計畫或設計無情地訪談你,一次問一個問題,直到你跟 agent 達成共同理解 —— 過程中同時把用語跟決策寫下來。

這場 grilling **會留下紙本紀錄**。一般的訪談會磨利你的思考,然後 session 一結束就蒸發了;這個版本會在每個用語一確定下來,就立刻捕捉進 `CONTEXT.md` 詞彙表,並把難以回頭的決策記成 ADR。這份共識能撐過這場對話本身,不會只活在你腦子裡。

## When to reach for it

你打 `/grill-with-docs` 來觸發它 —— agent 不會自己去找它。

在一項變動剛開始、計畫還很模糊、domain 用語還沒定案時就用它,在任何程式碼存在之前,先對兩者都做壓力測試。如果你只想要訪談、不需要那些產物,用 [grilling](https://aihero.dev/skills-grilling);如果計畫已經很清楚,只是需要確定或記錄用語,用 [domain-modeling](https://aihero.dev/skills-domain-modeling)。如果這個變動大到一次 session 裝不下,而且路線還很模糊 —— 一個全新的專案、一個巨大的功能建置 —— 從更上游的 [wayfinder](https://aihero.dev/skills-wayfinder) 開始:它會把這份工作規劃成一張決策地圖,等路線清楚了再交還給這條主流程。

## Prerequisites

這個 skill 是有狀態的 —— 它會在 grill 的過程中寫進你的 repo。確定下來的用語會落在根目錄的 `CONTEXT.md` 詞彙表(如果 `CONTEXT-MAP.md` 標記這是個多 context 的 repo,就落在相關 context 自己的 `CONTEXT.md`),真正難以回頭的決策會以 ADR 的形式落在 `docs/adr/` 底下。兩者都是懶惰式建立的 —— 在第一個用語或決策結晶之前什麼都不存在 —— 所以你不用事先搭好任何架子,但你得在一個可以安全寫入這些檔案的地方。

## The grill

它的引擎是一場 **grill**:無情地、一次一個問題地走過決策樹,先解決決策之間的依賴關係才往下走,每個問題都會附上一個建議答案。codebase 能回答的問題,就靠讀 codebase 來回答,不會拿去問你。

讓這個版本自成一個 skill 的,是答案的去處。隨著 grill 進行,模糊的用語會被磨利成標準用語,就地寫進詞彙表 —— 不是留到最後才批次寫。詞彙表會維持是一份詞彙表:純用語,沒有實作細節,不是 spec。ADR 只會少量出現,只有當一個決策難以回頭、沒有背景脈絡會讓人意外,而且是真正取捨的結果時才會寫。多數 session 產出的是一份更銳利的詞彙表,以及很少甚至沒有 ADR,而這正是設計上想要的樣子。

## It's working if

- 它一次問一個問題然後等待,而不是一口氣丟一整份問卷。
- 用語一確定下來就立刻寫進 `CONTEXT.md`,用你專案自己的話寫。
- 它會去查 codebase,盡可能自己回答自己的問題。
- ADR 很少出現 —— 你不會被要求為可逆的選擇蓋橡皮圖章。

## Where it fits

`grill-with-docs` 是主要建置鏈的開頭一步:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它排在最前面,在任何東西被寫成 spec 之前:它產出的共同理解與底定的詞彙,之後會被 [to-spec](https://aihero.dev/skills-to-spec) 整理成 spec,而不用再訪談你一次。它親近的鄰居是 [grilling](https://aihero.dev/skills-grilling)(同一場訪談,但不留文件)與 [domain-modeling](https://aihero.dev/skills-domain-modeling)(它驅動的詞彙表加 ADR 紀律)。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
