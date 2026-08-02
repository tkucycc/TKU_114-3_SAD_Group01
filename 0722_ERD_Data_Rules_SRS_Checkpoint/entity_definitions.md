
# 實體定義表 (Entity Definitions)

| 實體英文名稱            | 中文名稱 | 業務用途                                   | 主鍵 (PK)      | 重要屬性                                                           | 資料來源     |
| :---------------------- | :------- | :----------------------------------------- | :------------- | :----------------------------------------------------------------- | :----------- |
| **OrderSession**  | 揪團房間 | 保存一次揪團活動之房間狀態、店家與主揪資訊 | `room_id`    | `shop_name`, `host_name`, `is_closed`, `created_at`        | FR-01, BR-01 |
| **OrderDetail**   | 點單明細 | 保存團員於特定房間內點選之飲品加料與金額   | `detail_id`  | `room_id`, `user_id`, `item_name`, `subtotal`, `is_paid` | FR-02, BR-02 |
| **MenuItem**      | 飲品菜單 | 提供可點選之飲品品項與基礎單價             | `item_id`    | `shop_name`, `item_name`, `base_price`                       | 菜單資料     |
| **OptionAddon**   | 配料選項 | 提供客製化加價配料選項（如珍珠、椰果）     | `addon_id`   | `addon_name`, `extra_price`                                    | 菜單資料     |
| **PaymentRecord** | 付款標記 | 記錄主揪對團員線下收款之勾選狀態           | `payment_id` | `detail_id`, `is_paid`, `updated_at`                         | FR-05        |
