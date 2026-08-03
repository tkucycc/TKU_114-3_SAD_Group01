
# 跨模型一致性矩陣 (Cross-Model Consistency Matrix)

| 業務情境           | Use Case | DFD 處理 | ERD 欄位                   | Class 類別與方法                        | Sequence 訊息         | State 轉移       | main.py 實作                 | 測試案例 | 一致性         |
| :----------------- | :------- | :------- | :------------------------- | :-------------------------------------- | :-------------------- | :--------------- | :--------------------------- | :------- | :------------- |
| **建立房間** | UC-01    | P1.0, D1 | `OrderSession.room_id`   | `SessionControl.createSession()`      | `createSession`     | `-> Open`      | `/api/room/create`         | TC-M-01  | **一致** |
| **選購點餐** | UC-02    | P2.0, D2 | `OrderDetail.subtotal`   | `OrderControl.processOrder()`         | `processOrder`      | `Open`保持     | `/api/room/{id}/order`     | TC-M-02  | **一致** |
| **精算金額** | UC-02    | P2.0     | `OrderDetail.subtotal`   | `PricingService.calculateSubtotal()`  | `calculateSubtotal` | N/A              | 加料計算邏輯                 | TC-M-03  | **一致** |
| **一鍵結單** | UC-04    | P3.0, D1 | `OrderSession.is_closed` | `OrderSession.close()`                | `closeSession`      | `Open->Closed` | `is_closed=True`           | TC-S-01  | **一致** |
| **鎖單攔截** | UC-04    | P3.0     | `OrderSession.is_closed` | `OrderSession.canAcceptOrders()`      | `HTTP 403`          | `Closed`保持   | `raise HTTPException(403)` | TC-E-01  | **一致** |
| **店家總單** | UC-05    | P4.0, D2 | `OrderDetail.itemName`   | `ReportService.generateShopSummary()` | `getShopSummary`    | `Closed`       | `/summary` API             | TC-M-04  | **一致** |
| **對帳勾選** | UC-06    | P5.0, D2 | `OrderDetail.is_paid`    | `OrderDetail.markAsPaid()`            | `markAsPaid`        | N/A              | `/pay` API                 | TC-M-05  | **一致** |
