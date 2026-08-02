
# DFD / ERD / 原型假資料一致性矩陣

| 業務概念  | DFD 位置 | ERD 實體 / 屬性            | 原型假資料 (main.py)     | 計算與業務規則                | 一致性判斷         |
| :-------- | :------- | :------------------------- | :----------------------- | :---------------------------- | :----------------- |
| 房間 UUID | D1, P1.0 | `OrderSession.room_id`   | `session["room_id"]`   | 36 字元 UUID 唯一鍵           | **完全一致** |
| 鎖定狀態  | D1, P3.0 | `OrderSession.is_closed` | `session["is_closed"]` | `True` 阻斷後端 POST 寫入   | **完全一致** |
| 個人點單  | D2, P2.0 | `OrderDetail`            | `orders[user_id]`      | 學號為 key 避免重複點單       | **完全一致** |
| 計價金額  | D2, P2.0 | `OrderDetail.subtotal`   | `order["subtotal"]`    | 飲品底價 + 加料價 (100% 精確) | **完全一致** |
| 收款狀態  | D2, P5.0 | `OrderDetail.is_paid`    | `order["is_paid"]`     | 布林勾選標記                  | **完全一致** |
