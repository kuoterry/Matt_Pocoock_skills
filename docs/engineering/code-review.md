Quickstart:

```bash
npx skills add mattpocock/skills --skill=code-review
```

```bash
npx skills update code-review
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/code-review)

## What it does

`code-review` 審查 `HEAD` 跟你指定的一個固定點(一個 commit、branch、tag,或 merge-base)之間的 diff,沿著兩條各自獨立的軸線:**Standards**(這段程式碼有沒有遵守這個 repo 記載的慣例?)與 **Spec**(它有沒有實作出原始 issue 或 spec 要求的東西?)。它把每一軸都跑成各自獨立的平行 sub-agent,並排呈現結果。它絕不會把兩組發現合併或重新排序 —— 保持分開就是重點所在,因為一個變動可能一軸過、另一軸沒過,而單一混合過的結論會讓其中一個蓋掉另一個。

## When to reach for it

打 `/code-review`,或者當你要求審查一個 branch、一個 PR、進行中的變動,或任何「自 X 以來」的東西時,agent 會自動找上它。

當有一份 diff 要對照一個已知良好的點來判斷,而你想讓兩個問題 —— *做得對不對?* 跟 *做的是不是對的東西?* —— 各自獨立回答時,就用它。它是在建置迴圈的最後一步跑的;真正要用測試先行的方式寫程式碼,用 [tdd](https://aihero.dev/skills-tdd);要把整份 spec 建成程式碼,用 [implement](https://aihero.dev/skills-implement),它在 commit 前也會自己跑一輪 `/code-review`。

## Prerequisites

**Spec** 這一軸需要有地方能找到原始的 spec —— commit 訊息裡的 issue 參照、你傳進去的路徑,或是 `docs/`/`specs/` 底下的一份 spec。這條 issue-tracker 的接線來自 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills);找不到 spec 時,Spec 這一軸就會直接略過並說明原因。**Standards** 這一軸不需要任何前置設定 —— 就算 repo 完全沒記載任何慣例,它也一律內建一套 Fowler 程式碼異味基準。

## 兩軸,絕不合併

這個 skill 的核心概念是**兩軸**。**Standards** 問的是這份 diff 有沒有照這個 repo 寫程式碼的方式來 —— 它的 `CODING_STANDARDS.md` 或 `CONTRIBUTING.md`,再加上一套固定的、約 12 種 Fowler 程式碼異味基準(Mysterious Name、Duplicated Code、Feature Envy、Data Clumps……)。有兩條規則讓這套基準用起來安全:repo 記載的慣例永遠優先於它,而且每一種異味都是判斷題,絕不是硬性違規。**Spec** 問的是另一個獨立問題 —— 這段程式碼有沒有做到 issue 或 spec 真正要求的事,沒有漏掉需求,也沒有偷偷夾帶範圍外的東西?

它們以平行 sub-agent 執行,確保彼此不會污染對方的 context,最終報告會用各自獨立的 `## Standards` 與 `## Spec` 標題呈現,每一軸各有摘要。刻意不在兩軸之間選出單一贏家。

## It's working if

- 它會先釘住並確認固定點(`git rev-parse`),遇到爛的 ref 或空的 diff 會直接快速失敗,而不是在 sub-agent 裡面才爆掉。
- Standards 與 Spec 的發現會分成兩個獨立的區塊出現,各自引用自己的來源 —— 一邊是 repo 慣例或基準異味,另一邊是引用的 spec 原文。
- 找不到 spec 時,Spec 這一軸會回報「no spec available」,而不是自己捏造需求。

## Where it fits

`code-review` 是主要建置鏈末端的審查步驟:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它最近的鄰居是 [implement](https://aihero.dev/skills-implement),它驅動整個建置過程,並在 commit 前呼叫這個 skill 做自己的審查;往上游看,它拿來核對的 spec 是由 [to-spec](https://aihero.dev/skills-to-spec) 與 [to-tickets](https://aihero.dev/skills-to-tickets) 產生的。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
