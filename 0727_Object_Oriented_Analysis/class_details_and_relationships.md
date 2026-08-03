
# 類別明細與關係表

| 類別 A              | 關係類型    | 類別 B             | A端多重性 | B端多重性 | 業務規則依據                                           | 外來鍵 / 參考          |
| :------------------ | :---------- | :----------------- | :-------- | :-------- | :----------------------------------------------------- | :--------------------- |
| `SessionBoundary` | Association | `SessionControl` | `1`     | `1`     | 介面將開團/結單動作交由 SessionControl 協調            | 方法呼叫               |
| `OrderBoundary`   | Association | `OrderControl`   | `1`     | `1`     | 介面將點餐動作交由 OrderControl 協調                   | 方法呼叫               |
| `SessionControl`  | Association | `OrderSession`   | `1`     | `0..*`  | 一個 Control 可管理多個房間實體                        | `roomId`             |
| `OrderControl`    | Association | `PricingService` | `1`     | `1`     | OrderControl 依賴 PricingService 計價                  | 依賴注入               |
| `OrderSession`    | Composition | `OrderDetail`    | `1`     | `0..*`  | **BR-01：** 點單強烈依附房間，房間刪除明細亦消失 | `OrderDetail.roomId` |
