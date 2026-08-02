

# 系統分析與設計：0722 實體關係圖 (ERD)、資料規則與 SRS v1 整合成果

* **課程名稱：** 系統分析與設計
* **日期：** 115/07/22
* **小組名稱：** group01
* **專案名稱：** 團訂飲料系統
* **組員與分工：** 陳昱丞 (負責 SA&D ERD 資料模型建構、M:N 關聯拆解、正規化分析、SRS v1 規格書整編與追溯維護)
* **GitHub 儲存庫：** https://github.com/tku-im-sad/beverage-group-buying-system
* **成果資料夾：** `0722_ERD_Data_Rules_SRS_Checkpoint`

## 📁 7/22 成果檔案架構與導覽

* [實體候選表 (entity_candidate_list.md)](./entity_candidate_list.md)
* [實體定義表 (entity_definitions.md)](./entity_definitions.md)
* [屬性字典 (attribute_dictionary.md)](./attribute_dictionary.md)
* [關係與業務規則表 (relationship_business_rules.md)](./relationship_business_rules.md)
* [正規化與 M:N 拆解說明 (normalization_and_data_issues.md)](./normalization_and_data_issues.md)
* [基數與資料規則檢核 (data_rule_cardinality_check.md)](./data_rule_cardinality_check.md)
* [DFD/ERD/原型一致性矩陣 (dfd_erd_mock_data_consistency.md)](./dfd_erd_mock_data_consistency.md)
* [軟體需求規格書 v1.0 (srs_v1.md)](./srs_v1.md)
* [基準版本紀錄 (baseline_record.md)](./baseline_record.md)
* [待確認問題清單 (open_issues.md)](./open_issues.md)
* [需求追溯矩陣 (traceability_matrix.md)](./traceability_matrix.md)
* [期中影片建議清單 (midterm_video_content_suggestions.md)](./midterm_video_content_suggestions.md)
* [程式碼代理提示詞 (code_agent_prompts.md)](./code_agent_prompts.md)
* [程式碼代理執行紀錄 (code_agent_log.md)](./code_agent_log.md)

# 系統分析與設計：0721 資料流程圖、資料流分析與資料字典成果報告

* **課程名稱：** 系統分析與設計
* **日期：** 115/07/21
* **小組名稱：** group01
* **專案名稱：** 團訂飲料系統
* **組員與分工：** 陳昱丞
* **GitHub 儲存庫：** https://github.com/tku-im-sad/beverage-group-buying-system
* **成果資料夾：** `0721_DFD_Data_Flow_Analysis`

---

## A. 分析基準表

| 成果類型             | 版本或連結 | 本次使用範圍                                     | 待確認問題 |
| :------------------- | :--------- | :----------------------------------------------- | :--------- |
| 專案章程             | v2.0       | 團訂飲料系統核心範圍（開團、選購買、鎖單、對帳） | 無         |
| 功能性需求與業務規則 | v1.0       | FR-01 至 FR-05、BR-01 至 BR-03                   | 無         |
| 使用案例與描述       | v2.0       | UC-01 至 UC-07、UC-04 描述                       | 無         |
| 目標流程             | v2.0       | TO-BE 泳道流程圖                                 | 無         |
| 流程資料交換表       | v1.0       | 8 筆核心流程資料交換                             | 無         |
| 實作品程式碼         | main.py    | FastAPI 後端 API 與 In-memory DB 結構            | 無         |

---

## B. 外部實體與資料交換清單 (至少 3 個外部實體 / 8 筆資料交換)

### 1. 外部實體清單

* **E1 主揪 (Host)：** 發起揪團、設定店家、執行結單鎖定與對帳管理之使用者（位於系統邊界外）。
* **E2 一般團員 (Participant)：** 透過分享連結進入房間、點餐客製化與修改點單之使用者（位於系統邊界外）。
* **E3 外部店家 (External Shop)：** 接收彙總總單並製作飲料之實體店家（位於系統邊界外，本期僅接受主揪口頭報單）。

### 2. 資料交換清單

| 編號            | 外部實體    | 方向        | 資料流名稱     | 內容摘要                                               | 對應流程 | 對應需求 |
| :-------------- | :---------- | :---------- | :------------- | :----------------------------------------------------- | :------- | :------- |
| **EX-01** | E1 主揪     | 輸入        | 開團資訊       | 店家名稱 (shop_name)、主揪暱稱 (host_name)             | 1.0      | FR-01    |
| **EX-02** | E1 主揪     | 輸出        | 房間連結資訊   | UUID 房間網址 (/room/{uuid})                           | 1.0      | FR-01    |
| **EX-03** | E2 一般團員 | 輸入        | 點餐提交資料   | 學號 (user_id)、暱稱 (user_name)、品項、冰甜客製、加料 | 2.0      | FR-02    |
| **EX-04** | E2 一般團員 | 輸出        | 個人點餐回應   | 點餐成功訊息、個人小計金額 (subtotal)                  | 2.0      | FR-02    |
| **EX-05** | E1 主揪     | 輸入        | 結單指令       | 房間 UUID、結單觸發訊號 (is_closed=True)               | 3.0      | FR-03    |
| **EX-06** | E1 主揪     | 輸出        | 店家彙總總單   | 依飲品/冰甜/加料合併後之品項與總杯數                   | 4.0      | FR-04    |
| **EX-07** | E1 主揪     | 輸出        | 團員收款對帳單 | 團員清單、每人應付金額、付款標記勾選狀態               | 5.0      | FR-05    |
| **EX-08** | E3 外部店家 | 輸出 (線下) | 電話報單內容   | 飲料品項、總杯數、甜度冰塊客製需求                     | 4.0      | FR-04    |

---

## C. 系統環境圖 (Context Diagram)

系統環境圖將整套「團訂飲料系統」視為單一總處理程序 `0`，劃分出系統內部與外部實體的資料流邊界。

```mermaid
flowchart LR
    E1["E1 主揪"]
    E2["E2 一般團員"]
    E3["E3 外部店家"]
    P0(("0 團訂飲料系統"))

    E1 -->|"開團資訊"| P0
    P0 -->|"房間連結資訊"| E1
  
    E2 -->|"點餐提交資料"| P0
    P0 -->|"個人點餐回應"| E2
  
    E1 -->|"結單指令"| P0
    P0 -->|"店家彙總總單"| E1
    P0 -->|"團員收款對帳單"| E1
  
    P0 -.->"電話報單內容 (線下)"| E3
```
