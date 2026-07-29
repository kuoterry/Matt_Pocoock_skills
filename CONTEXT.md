# Matt Pocock Skills

一組 Claude Code 載入的 agent skill 集合(slash command 與行為模式)。skill 依 bucket 分類,由 `/setup-matt-pocock-skills` 產生的各 repo 專屬設定所使用。

## 用語

**Issue tracker**:
承載一個 repo 所有 issue 的工具 —— GitHub Issues、Linear、本地 `.scratch/` markdown 慣例,或類似工具。`to-tickets`、`to-spec`、`triage`、`qa` 等 skill 會對它讀寫。
_避免使用_:backlog manager、backlog backend、issue host

**Issue**:
**Issue tracker** 內部單一被追蹤的工作單位 —— 一個 bug、任務、spec,或由 `to-tickets` 產生的一個 slice。
_避免使用_:ticket(僅在引用外部系統本身就稱其為 ticket 時使用,或指 **Decision ticket** —— 見下方)

**Decision ticket**:
`wayfinder` 用語,是 `wayfinder:map` 底下的一個子 **Issue**,內容是一個「問題」,其解法是一個決策而非要執行的建置 slice。**decision** 這個限定詞讓它與一般實作 ticket 區隔開;`wayfinder` 先引入此詞,之後就簡稱 "ticket"。

**Triage role**:
在 triage 過程中套用到某個 **Issue** 上的一個標準狀態機標籤(如 `needs-triage`、`ready-for-afk`)。每個 role 透過 `docs/agents/triage-labels.md` 對應到 **Issue tracker** 裡實際的標籤字串。

## 關係

- 一個 **Issue tracker** 裡有許多 **Issue**
- 一個 **Issue** 在同一時間只帶一個 **Triage role**
- 一個 **Decision ticket** 是一種 **Issue**(`wayfinder:map` 的子項)

## 已標記的模糊用語

- "backlog" 過去同時被用來指「承載 issue 的工具」與「工具裡的工作內容本身」兩種意思 —— 已解決:工具本身統一稱 **Issue tracker**;"backlog" 不再作為此 repo 的定義用語使用。
- "backlog backend" / "backlog manager" —— 已解決:一律併入 **Issue tracker**。
