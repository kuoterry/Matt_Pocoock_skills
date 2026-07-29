Quickstart:

```bash
npx skills add mattpocock/skills --skill=implement
```

```bash
npx skills update implement
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/implement)

## What it does

`implement` 建構一份 spec 或一組 ticket 裡描述的工作 —— 透過 test-driven development、型別檢查,以及完整的測試套件把它跑完,再交接給審查,並 commit 進目前的 branch。

它**不會**決定要建什麼。spec 已經定案,接縫也已經談好;`implement` 是執行那份計畫,而不是重新打開它。它是那雙手,不是那顆腦袋 —— 思考的部分在上游已經做完了。

## When to reach for it

你打 `/implement` 來觸發它 —— agent 不會自己去找它。

當工作已經寫成一份 spec,或已經拆成一組 ticket,而你準備好把它變成程式碼時就用它。如果 spec 還不存在,先寫出來 —— 用 [to-spec](https://aihero.dev/skills-to-spec),或用 [to-tickets](https://aihero.dev/skills-to-tickets) 把一份 spec 拆成 ticket。如果你只是想在沒有完整 spec 的情況下,用測試先行的方式建東西,直接切到 [tdd](https://aihero.dev/skills-tdd)。

## 事先談好的接縫

`implement` 運作所依靠的概念是**接縫(seam)**—— 一個功能被測試的那個穩定介面,在任何程式碼寫出來之前就先選好。它不會在建置過程中臨時發明接縫;它用的是已經選好的那些(在 [to-spec](https://aihero.dev/skills-to-spec) 期間選的),並透過 [tdd](https://aihero.dev/skills-tdd) 針對它們寫測試。在事先談好的接縫上工作,才能讓實作保持誠實:測試瞄準的是穩固的東西,所以底下的程式碼可以變動,而測試不用跟著變。

圍繞這個核心,它讓迴圈保持緊實:常常做型別檢查、邊做邊跑單一測試檔、最後跑一次完整套件 —— 然後用一輪審查,再 commit 進目前的 branch 收尾。

## Where it fits

`implement` 是主要鏈末段、就在審查之前的建置步驟:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

在工作已經寫成 spec、排好順序之後再用它,而不是之前。它的重要鄰居是 [to-tickets](https://aihero.dev/skills-to-tickets),它產出的那些 ticket(每個都宣告自己的 blocking 關係)就是它要一一做完的工作;還有 [tdd](https://aihero.dev/skills-tdd),它內部驅動 `tdd` 在每個接縫上寫測試,然後才跑自己的 [code-review](https://aihero.dev/skills-code-review) 並 commit。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
