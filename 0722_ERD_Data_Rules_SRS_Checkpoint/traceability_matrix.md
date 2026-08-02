
# 需求追溯矩陣 (Traceability Matrix)

| 需求編號        | 需求來源 | 業務規則 (BR) | 使用案例 | DFD 處理 | ERD 實體/欄位              | API / 實作品                | 驗收條件 | 狀態           |
| :-------------- | :------- | :------------ | :------- | :------- | :------------------------- | :-------------------------- | :------- | :------------- |
| **FR-01** | SRC-01   | BR-ACT-01     | UC-01    | P1.0, D1 | `OrderSession.room_id`   | `/api/room/create`        | AC-01-01 | **一致** |
| **FR-02** | SRC-02   | BR-REG-02     | UC-02    | P2.0, D2 | `OrderDetail.subtotal`   | `/api/room/{id}/order`    | AC-02-01 | **一致** |
| **FR-03** | SRC-09   | BR-01         | UC-04    | P3.0, D1 | `OrderSession.is_closed` | `if is_closed: raise 403` | AC-03-02 | **一致** |
| **FR-04** | SRC-04   | BR-ACT-02     | UC-05    | P4.0, D2 | `OrderDetail.item_name`  | `/api/room/{id}/summary`  | AC-04-01 | **一致** |
| **FR-05** | SRC-05   | BR-REG-03     | UC-06    | P5.0, D2 | `OrderDetail.is_paid`    | `/api/room/{id}/pay`      | AC-05-01 | **一致** |
