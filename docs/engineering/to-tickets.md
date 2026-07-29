Quickstart:

```bash
npx skills add mattpocock/skills --skill=to-tickets
```

```bash
npx skills update to-tickets
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets)

## What it does

`to-tickets` 把一份計畫、spec,或目前的對話拆成一組**ticket**——每張都是一個 tracer-bullet 垂直切片——再發佈到你設定好的 tracker,每張 ticket 都宣告是哪些 ticket 在擋著它。

每張 ticket 都是一發**tracer bullet**——一個薄薄的*垂直*切片,端到端切穿所有整合層(schema、API、UI、測試),絕不是單一層的水平切片。一個做完的切片自己就能展示或驗證,這正是讓每張 ticket 能安心交給 agent 的原因。

## When to reach for it

你打 `/to-tickets` 來觸發它——agent 不會自己去找它。

當你已經有一份談好的計畫或寫好的 spec,想把它拆成 ticket 時就用它。指向這場對話,或傳入一份 spec 或 issue 參照,它會先抓取內文與留言。如果這項變動還沒被寫成 spec,先產出一份——用 [to-spec](https://aihero.dev/skills-to-spec)。

## Prerequisites

`to-tickets` 會發佈進你的 issue tracker,所以 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 必須已經先幫這個 repo 設定好 tracker 跟它的 triage 標籤詞彙。在真實的 tracker 上,它發佈時會自己套用 ready-for-agent 標籤。

## 一份產物,兩種讀法

blocking 關係就是整個重點所在。它們讓同一組 ticket,依 tracker 不同而有兩種讀法:

- **本地檔案** → `.scratch/<feature>/issues/` 底下一個 ticket 一個檔,依阻擋關係編號、擋人的排前面,關係用文字寫出來。你由上而下手動一一處理,全程參與。
- **真實 tracker(GitHub、Linear)** → 一個 ticket 對應一個 issue,關係用原生的 blocking 連結(或 sub-issue)表示。任何一張擋它的 ticket 都做完的,就位在**前緣(frontier)**上,可以直接被領走——所以可以同時跑好幾個 agent。

不管用哪種媒介,關係都活在 ticket 裡;媒介只決定有沒有東西能平行去動它們。`to-tickets` 產出的是這份產物——你要怎麼跑它(手動依序,還是一支平行的艦隊)由你決定。

## 垂直切片,不是水平切片

整個 skill 繞著一個區別轉。一個**水平**切片出貨的是變動的一整層——所有 schema,或所有 API——在每一層都上線之前,什麼都不會動。一個**垂直**切片,也就是 tracer bullet,一次出貨一條穿過*每一層*的窄路徑,所以它一做完就能展示。

在切之前,`to-tickets` 會先找有沒有 prefactoring 的機會——「先讓變動變簡單,再做那個簡單的變動」——並把那份工作排在最前面。接著它會在發佈任何東西之前,針對拆分方式盤問你(粒度、阻擋關係、要合併還是拆開哪些),並先發佈擋人的 ticket,讓每張 ticket 的「Blocked by」都能參照到一張真實存在的 ticket。

## 大範圍重構的例外

有一種形狀會打破 tracer-bullet 規則:一個**大範圍重構**——一個單一的機械式變動(重新命名一個欄位、給一個共用符號改型別),它的**波及範圍(blast radius)**擴散到整個 codebase,所以一次編輯就會同時弄壞上千個呼叫點,沒有任何垂直切片能保持綠燈上線。`to-tickets` 改用**expand–contract** 的方式切它:expand(在舊寫法旁邊加上新寫法,不弄壞任何東西)、migrate(依波及範圍大小分批,把呼叫點搬過去,一批一張 ticket,過程中 CI 全程綠燈,因為舊寫法還在),然後 contract(等沒有呼叫者留著舊寫法後,把它刪掉)。當連分批都沒辦法各自保持綠燈時,它們會共用一個整合 branch,全部一起擋住最後一張「整合並驗證」的 ticket,而綠燈只保證在那裡出現。

## Where it fits

`to-tickets` 是主要建置鏈裡的一步:

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review
```

它介於 [to-spec](https://aihero.dev/skills-to-spec)(交給它一份定案、附 user story 可供切分的 spec)與 [implement](https://aihero.dev/skills-implement)(建構每張 ticket,內部驅動 [tdd](https://aihero.dev/skills-tdd) 以測試先行的方式寫測試,再跑它的 [code-review](https://aihero.dev/skills-code-review))之間。一次用一張全新的 context 處理前緣上的一張 ticket,做完就清空再繼續。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
