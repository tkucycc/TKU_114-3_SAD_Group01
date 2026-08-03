
# 模型-畫面-資料-驗收一致性矩陣

| 需求編號        | Use Case | OOA 類別/操作                     | 畫面編號 | 呈現欄位/資料                            | 驗收條件 | 可用性測試任務 | 一致性         |
| :-------------- | :------- | :-------------------------------- | :------- | :--------------------------------------- | :------- | :------------- | :------------- |
| **FR-01** | UC-01    | `SessionControl.createSession`  | UI-01    | `shop_name`, `room_id`               | AC-01-01 | P-T01          | **一致** |
| **FR-02** | UC-02    | `OrderControl.processOrder`     | UI-02    | `user_id`, `item_name`, `subtotal` | AC-02-01 | P-T01          | **一致** |
| **FR-03** | UC-04    | `OrderSession.close()`          | UI-02L   | `is_closed=True`, 403 Error            | AC-03-02 | P-T02          | **一致** |
| **FR-04** | UC-05    | `ReportService.generateSummary` | UI-03    | `item_name`, `total_qty`             | AC-04-01 | P-T03          | **一致** |
| **FR-05** | UC-06    | `OrderDetail.markAsPaid()`      | UI-03    | `user_id`, `subtotal`, `is_paid`   | AC-05-01 | P-T03          | **一致** |
