Quickstart:

```bash
npx skills add mattpocock/skills --skill=wayfinder
```

```bash
npx skills update wayfinder
```

[Source](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder)

## What it does

`wayfinder` 拿一件大到一次 agent session 裝不下、還籠罩在迷霧裡、從這裡到目標的路還看不見的工作,把它畫成你 issue tracker 上一張**共用地圖**、由一堆**decision ticket** 組成,再一次解決一張,直到路線清楚為止。它**只規劃,不動手做**:每張 ticket 解決的是一個決策——一個要被確定下來的問題,不是一段要執行的建置切片——地圖做完的定義,是在有人真正動手去蓋這個東西之前,已經沒有東西需要再決定了——所以它產出的是決策,不是交付物。

## When to reach for it

你打 `/wayfinder` 來觸發它——agent 不會自己去找它。

當一件工作**大到一次 agent session 裝不下**、通往它**目的地**的路線還籠罩在迷霧裡時就用它——你能感覺到這件工作的輪廓,但還沒辦法把它寫成一份 spec 或計畫。要把一條*已經清楚*的討論串變成 spec,用 [to-spec](https://aihero.dev/skills-to-spec);要把一份*已經想清楚*的計畫拆成可建置的 ticket,用 [to-tickets](https://aihero.dev/skills-to-tickets)。wayfinder 站在這兩者的上游:當迷霧濃到沒辦法直接寫 spec 時,就跑它。

## Prerequisites

地圖跟它的 ticket 都活在這個 repo 的 issue tracker 上,所以 wayfinder 需要 [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills) 先接好的 tracker 線路——它會種下一個「Wayfinding operations」段落,描述地圖、子 ticket、blocking,以及 frontier 查詢在 GitHub、GitLab,或本地 markdown 上分別怎麼表達。沒有這份文件時,wayfinder 預設用本地 markdown 地圖。

## 地圖是索引,迷霧是前緣

**地圖**是單一一個 `wayfinder:map` issue,它的 ticket 就是它的子 issue——一個整個團隊都能盯著看的共用網址。它是一份**索引,不是儲存庫**:每個決策都恰好活在一個地方(它自己的 ticket),地圖只做摘要跟連結,絕不重複陳述內容。一次 session 會先用低解析度載入地圖,再按需求放大看個別 ticket。

在活著的 ticket 之外,還有**戰爭迷霧**——你能感覺得到即將出現、但還沒能定位的決策。判斷一件事是一張 ticket 還是還算迷霧的測試,是你*現在*能不能精確陳述這個問題,而不是你能不能回答它。解決一張 ticket 會把它前面的迷霧清開,把現在能被明確表述的東西**畢業**成全新的 ticket。**前緣(frontier)**是那些開著、沒被擋、還沒被人領走的 ticket——已知範圍的邊界——tracker 原生的 blocking 功能會把它視覺化呈現出來,所以你不用打開地圖就能看出哪些能拿去做。迷霧只會朝著**目的地**方向聚集;超出目的地的工作會被判為**範圍外**,關閉,永遠不會畢業。

每張 ticket 都是 **HITL**(human in the loop——grilling、prototype)或 **AFK**(agent 自己來——research);一張 HITL ticket 只能透過一場真人參與的來回交流解決,所以 agent 絕不會自問自答。research 仍然是一張真正的 ticket——一個下游決策掛著等的共用阻擋者——但因為它是 AFK,一次 session 不會停下來自己讀:它會發動一個 `/research` **subagent** 平行把這張 ticket 燒完,讓前緣保持推進速度,並把結果記錄在一條用完即丟的 `research/<name>` branch 上。

## It's working if

- 第一個動作是先講清楚**目的地**——在任何 ticket 存在之前——因為這定死了每張 ticket 要拿來衡量的範圍。
- 一張地圖就是一個 `wayfinder:map` issue;ticket 是它的子 issue,一律用**名字**指稱,絕不是光禿禿的 `#42`。
- 一次 session 最多解決**一張** ticket(research ticket 除外),把答案記成一則解決留言,關閉這張 ticket,並在《目前為止的決策》附加一行指標。
- 如果一開始的 grill 完全**沒發現迷霧**,它就會停下來告訴你,這趟路程小到可以跳過地圖。

## Where it fits

`wayfinder` 是給大點子走的**匝道**:一件大到、模糊到沒辦法一次坐下來寫成 spec 的工作,會產出一張迷霧已清開的決策地圖,再併回主要建置流程。等迷霧被推開、路線清楚了,就交接給 [to-spec](https://aihero.dev/skills-to-spec) 去安排跨多個 session 的建置(或者,如果這件事其實不大,就直接動手實作)。它靠 [grilling](https://aihero.dev/skills-grilling) 與 [domain-modeling](https://aihero.dev/skills-domain-modeling) 來解決個別 ticket,靠 [prototype](https://aihero.dev/skills-prototype) 與 [research](https://aihero.dev/skills-research) 處理需要它們的那類 ticket。不確定該用哪個 skill 或流程時,[ask-matt](https://aihero.dev/skills-ask-matt) 會幫你導航。
