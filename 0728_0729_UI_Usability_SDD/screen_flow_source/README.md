
# 畫面流程圖 (Screen Flow) Mermaid 原始碼

```mermaid
flowchart LR
    UI01[UI-01 首頁開團] -->|建立房間| UI02[UI-02 點餐房間]
    UI02 -->|送出點餐| UI02S[UI-02S 點餐成功]
    UI02 -->|學號空白| UI02E[UI-02E 表單錯誤]
    UI02 -->|主揪點擊結單| UI03[UI-03 已結單對帳頁]
    UI03 -->|惡意團員強行提交| UI02L[UI-02L 鎖定停用頁 (403)]
    UI03 -->|主揪勾選收現| UI03P[UI-03P 付款狀態更新]
```


---

### 6. `0728_0729_UI_Usability_SDD/screen_inventory.md`

```markdown
# 畫面清單 (Screen Inventory)

| 畫面編號 | 畫面/狀態名稱 | 主要目的 | 核心呈現資料 | 包含介面狀態 | 來源/對應需求 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **UI-01** | 首頁開團頁 | 主揪發起新揪團 | 店家名稱、主揪暱稱 | Normal, Loading, Error | FR-01 |
| **UI-02** | 團員點餐房間 | 團員填單點餐 | 菜單、冰甜選項、加料複選、即時小計 | Normal, Disabled | FR-02, NFR-01 |
| **UI-02E** | 點餐表單錯誤狀態 | 防呆提示 | 學號紅框高亮、警示文字「請填寫學號」 | Error (保留已選配料) | BR-02 |
| **UI-02L** | 鎖定停用狀態 | 阻止結單後修改 | 「已結單」灰標籤、停用按鈕、403 提示 | Disabled, Permission Denied | FR-03, NFR-03 |
| **UI-03** | 店家總單與對帳頁 | 主揪訂餐與對帳 | 歸類總杯數清單、團員應付金額、付款 Checkbox | Normal, Loading | FR-04, FR-05 |
```
