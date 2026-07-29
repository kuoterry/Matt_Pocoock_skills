# 只有硬依賴才明講 `/setup-matt-pocock-skills` 指標

Engineering skill 依賴由 `/setup-matt-pocock-skills` 產生的、每個 repo 各自的設定(issue tracker、triage 標籤詞彙、domain 文件的存放方式)。有些 skill 沒有這份設定就沒辦法真正運作 —— 它們得發佈到某個特定的 issue tracker,或套用某個特定的標籤字串。另一些只是拿它來讓輸出更精準(詞彙、對 ADR 的認知),沒有這份設定也能優雅地降級運作。

我們把這些 skill 分成**硬依賴**與**軟依賴**兩種:

- **硬依賴**(`to-tickets`、`to-spec`、`triage`)—— 明講一句話:_「……應該已經提供給你了 —— 如果沒有,就跑一次 `/setup-matt-pocock-skills`。」_ 沒有這份對應關係,輸出的內容是錯的,不只是不夠精準而已。
- **軟依賴**(`diagnose`、`tdd`、`improve-codebase-architecture`)—— 只用模糊的 prose 提到「這個專案的 domain glossary」與「你正在動的這塊區域的 ADR」。就算文件不存在,skill 還是能運作;輸出只是不夠銳利而已。

這樣的區分讓軟依賴的 skill 保持精簡(省 token),也避免把 setup 指標的寫法生搬硬套到它其實沒發揮作用的地方。
