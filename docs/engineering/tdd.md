Quickstart:

```bash
npx skills add mattpocock/skills --skill=tdd
```

```bash
npx skills update tdd
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd)

## What it does

`tdd` 用測試先行的方式建構功能或修 bug,一次一個行為,透過紅-綠迴圈把程式碼逼出來。

它**不會**先把所有測試都寫完。先批次寫測試(「水平切片」)只會產出檢查*想像中*行為的測試——它們檢查的是東西的外形,對真正的變動反而變得遲鈍。`tdd` 走的是垂直切片:一個測試,再寫剛好夠讓它通過的程式碼,然後下一個測試,每一輪都靠上一輪教會你的東西往前走。測試只瞄準公開介面,所以底下的實作可以變動,測試不用跟著動。

## When to reach for it

打 `/tdd`,或者當任務吻合時 agent 會自動找上它——用測試先行的方式建功能、修 bug,或是你講「red-green-refactor」時。

當有一個具體的行為要建構,而你想要能撐過重構的測試時就用它。如果行為還沒定案,先確定 spec——用 [to-spec](https://aihero.dev/skills-to-spec)。當工作真正的重點是介面的形狀而不是測試時,用 [codebase-design](https://aihero.dev/skills-codebase-design);`tdd` 在規劃時會呼叫它取用深 module 的詞彙。

## 紅-綠,一次一個切片

核心概念是**紅-綠迴圈**:寫一個會失敗的測試(紅),加上剛好夠讓它通過的程式碼(綠),再對下一個行為重複——每一輪都靠上一輪教會你的東西往前走。第一輪是一發**tracer bullet**:一個測試,證明單一路徑能端到端跑通,然後你才從它往外擴建。因為程式碼是你剛寫的,你確切知道哪個行為重要、該怎麼驗證它——你絕不會在還沒搞懂測試結構之前,就先綁死自己去承諾那個結構,跑到自己車頭燈照不到的地方。

有兩條規則讓測試保持誠實。一個好測試讀起來像一份規格(「使用者能用有效的購物車結帳」),透過公開 API 走真實的程式碼路徑,所以重新命名一個內部函式絕不會弄壞它。以及,預期值要來自一個獨立的真相來源——一個已知正確的字面值、一個算過的範例、spec 本身——絕不用程式碼算它的同一種方式重算一次,那樣算出來的是一個**套套邏輯(tautological)**測試,靠自身結構就會通過,什麼都告訴不了你。

只有在整個套件是綠燈時才重構;紅燈時絕不重構。

## It's working if

- 它寫一個測試、讓它通過,然後才寫下一個——不是先一批測試,再一批程式碼。
- 測試命名的是行為,不是內部細節,重新命名一個內部東西不會弄壞它。
- 預期值是來自 spec 的字面值,不是用程式碼算它的同一種方式推導出來的數字。

## Where it fits

`tdd` 是主要建置鏈用來寫程式碼的紅-綠迴圈:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

[implement](https://aihero.dev/skills-implement) 是這條鏈的建置步驟,它在內部驅動 `tdd`,以測試先行的方式把每張 ticket 建出來,再交給 [code-review](https://aihero.dev/skills-code-review)——所以 `tdd` 是那個步驟*裡面*的引擎,而不是它自己獨立的一步。你也可以直接拿它來用,只要有一個具體行為要建、又不需要完整 spec 的時候。它另一個鄰居是 [codebase-design](https://aihero.dev/skills-codebase-design),它靠這個 skill 找出值得拿來測試的深 module 接縫。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
