Quickstart:

```bash
npx skills add mattpocock/skills --skill=diagnosing-bugs
```

```bash
npx skills update diagnosing-bugs
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnosing-bugs)

## What it does

`diagnosing-bugs` 針對難搞的 bug 與效能退化,跑一套有紀律的診斷迴圈 —— 建立重現方式、把它最小化、給假設排序、埋測,最後用一個回歸測試把修復鎖住。

在你手上有一個**緊迴圈(tight feedback loop)**之前 —— 一條已經能對*這個* bug 跑出紅燈的可執行指令 —— 它拒絕先提出假設。在那條指令存在之前就去讀程式碼、建立理論,正是這個 skill 要防止的那種失敗。沒有能亮紅燈的迴圈,就不診斷。

## When to reach for it

打 `/diagnosing-bugs`,或者當任務吻合時 agent 會自動找上它 —— 遇到「diagnose」/「debug this」,或是你回報有東西壞了、丟例外、失敗,或變慢時,它就會觸發。

難搞的情況就用它:第一眼看不出所以然的 bug、時有時無的 flaky 測試、在兩個已知良好的狀態之間悄悄爬進來的 regression。如果只是想做個用完即丟的東西來驗證一個設計問題,而不是在追一個缺陷,改用 [prototype](https://aihero.dev/skills-prototype)。

## 緊迴圈就是這個 skill 的核心

一旦你有了訊號,剩下的一切 —— 二分搜尋、假設檢驗、埋測 —— 都只是機械式的操作。所以這個 skill 把不成比例的心力都放在第一階段:建出一條會驅動真正 bug 路徑、斷言使用者確切症狀的通過/失敗指令,然後把它**收緊**到快、確定、agent 可以自己跑。一個要跑 30 秒、還會 flaky 的迴圈,幾乎跟沒有一樣;一個 2 秒、結果穩定的迴圈,才是除錯的超能力。

它給你一整套建這種迴圈的階梯 —— 失敗的測試、curl script、CLI diff、headless browser、重播的 trace、用完即丟的測試骨架、fuzz 迴圈、`git bisect run`、差異比對執行 —— 只有在萬不得已時,才退到需要人在迴圈裡的 bash script。對於非確定性的 bug,目標不是一個乾淨的重現,而是一個**更高的重現率**:反覆觸發、平行跑、加壓力,直到這個 flaky 情況變得可以除錯。

## It's working if

- 它會在提出理論*之前*先建好並跑一次重現指令 —— 並貼出執行方式與它跑出的紅燈輸出。
- 這個迴圈斷言的是你真正回報的那個症狀,不是附近某個看起來很像的失敗。
- 假設是以一份排過序、可被證偽的清單出現,在測試任何一個之前先給你看。
- 除錯用的埋測都有標記(`[DEBUG-...]`),在宣告完成前會被 grep 掉。

## Where it fits

`diagnosing-bugs` 是一個**隨時可以拿來用的獨立工具** —— 東西一壞掉你就切進去用,修好、加上回歸測試之後就跳出來。當它做完事後檢討,發現真正的問題是「沒有一個好的接縫能把這個 bug 鎖住」—— 問題出在程式碼,不是這個 bug 本身 —— 它會交接給 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)。不確定該用哪個 skill 時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
