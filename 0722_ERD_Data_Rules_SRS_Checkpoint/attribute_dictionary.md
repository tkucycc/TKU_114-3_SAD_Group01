
# 屬性字典 (Attribute Dictionary)

| 實體                   | 屬性名稱      | 中文名稱   | 鍵別         | 型態概念 | 必填 | 業務規則 / 允許值                         | 來源          |
| :--------------------- | :------------ | :--------- | :----------- | :------- | :--- | :---------------------------------------- | :------------ |
| **OrderSession** | `room_id`   | 房間 UUID  | **PK** | String   | 是   | 36 字元系統生成 UUID，唯一且不變          | FR-01         |
| **OrderSession** | `shop_name` | 店家名稱   | -            | String   | 是   | 預設為「50嵐」或「可不可」                | FR-01         |
| **OrderSession** | `is_closed` | 鎖定狀態   | -            | Boolean  | 是   | `True`: 已結單鎖定; `False`: 開放點餐 | FR-03, BR-01  |
| **OrderDetail**  | `detail_id` | 明細識別碼 | **PK** | String   | 是   | 系統單一明細唯一 UUID                     | FR-02         |
| **OrderDetail**  | `room_id`   | 關聯房間碼 | **FK** | String   | 是   | 必須參照存在的`OrderSession.room_id`    | BR-REG-01     |
| **OrderDetail**  | `user_id`   | 團員學號   | -            | String   | 是   | 學號欄位，開頭不可空白                    | BR-REG-02     |
| **OrderDetail**  | `subtotal`  | 個人小計   | -            | Integer  | 是   | `>= 0`，精確加總無浮點數誤差            | NFR-01, BR-03 |
| **OrderDetail**  | `is_paid`   | 收款狀態   | -            | Boolean  | 是   | `True`: 已付款; `False`: 未付款       | FR-05         |
