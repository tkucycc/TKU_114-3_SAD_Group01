
# 8 張 CRC 類別責任卡 (CRC Cards)

### CRC-01: SessionBoundary (邊界類別)

* **類別名稱：** `SessionBoundary` | **類型：** Boundary
* **主要責任：** 接收主揪開團與結單請求、渲染開團結果與對帳頁面、顯示結單成功或錯誤提示。
* **重要屬性：** `shopNameInput`, `hostNameInput`
* **主要操作：** `renderRoom()`, `displayClosedState()`, `showError(msg)`
* **協作者：** `SessionControl`
* **來源/理由：** UC-01, UC-04 / 隔離 UI 與商業邏輯。

### CRC-02: OrderBoundary (邊界類別)

* **類別名稱：** `OrderBoundary` | **類型：** Boundary
* **主要責任：** 接收團員點餐與客製化加料表單、渲染點餐成功回應與小計金額、停用已結單房間之按鈕。
* **重要屬性：** `userIdInput`, `selectedItem`, `addonsCheckboxes`
* **主要操作：** `submitOrder()`, `disableForm()`, `renderSubtotal(amount)`
* **協作者：** `OrderControl`
* **來源/理由：** UC-02, BR-01 / 提供團員點餐介面。

### CRC-03: SessionControl (控制類別)

* **類別名稱：** `SessionControl` | **類型：** Control
* **主要責任：** 協調開團流程、生成 UUID、觸發一鍵結單並將狀態鎖定指令下發至 `OrderSession`。
* **重要屬性：** `activeSessions`
* **主要操作：** `createSession(shop, host)`, `closeSession(roomId)`
* **協作者：** `OrderSession`, `SessionBoundary`
* **來源/理由：** UC-01, UC-04 / 協調開團與鎖定使用案例。

### CRC-04: OrderControl (控制類別)

* **類別名稱：** `OrderControl` | **類型：** Control
* **主要責任：** 協調點餐流程、向 `OrderSession` 查詢 `is_closed` 狀態、呼叫 `PricingService` 計算金額並建立 `OrderDetail`。
* **重要屬性：** `pricingService`
* **主要操作：** `processOrder(roomId, orderData)`, `validateState(roomId)`
* **協作者：** `OrderSession`, `OrderDetail`, `PricingService`
* **來源/理由：** UC-02, BR-02 / 協調點餐與鎖定攔截驗證。

### CRC-05: OrderSession (實體類別)

* **類別名稱：** `OrderSession` | **類型：** Entity
* **主要責任：** 保存房間生命週期、維護 `is_closed` 狀態、執行 `close()` 鎖定動作並阻斷非法修改。
* **重要屬性：** `roomId`, `shopName`, `hostName`, `isClosed`, `createdAt`
* **主要操作：** `close()`, `canAcceptOrders()`, `addOrderDetail(detail)`
* **協作者：** `OrderDetail`
* **來源/理由：** ERD OrderSession, BR-01 / 核心業務領域實體。

### CRC-06: OrderDetail (實體類別)

* **類別名稱：** `OrderDetail` | **類型：** Entity
* **主要責任：** 保存團員點單明細、客製化選項與金額小計、維護付款標記 (`isPaid`)。
* **重要屬性：** `detailId`, `roomId`, `userId`, `userName`, `itemName`, `subtotal`, `isPaid`
* **主要操作：** `markAsPaid()`, `updateOrder(newItem, newSubtotal)`
* **協作者：** `OrderSession`
* **來源/理由：** ERD OrderDetail, DR-04 / 點單紀錄實體。

### CRC-07: PricingService (領域服務類別)

* **類別名稱：** `PricingService` | **類型：** Entity / Domain Service
* **主要責任：** 封裝飲品底價與配料加價邏輯，計算 100% 精確且無浮點數累積誤差之金額。
* **重要屬性：** `menuPrices`, `addonPrices`
* **主要操作：** `calculateSubtotal(item, addons)`
* **協作者：** `OrderControl`
* **來源/理由：** NFR-01, BR-03 / 確保計算零誤差與內聚。

### CRC-08: ReportService (領域服務類別)

* **類別名稱：** `ReportService` | **類型：** Entity / Domain Service
* **主要責任：** 讀取已結單房間之明細，進行品項 Group By 歸類合併產出「店家總單」與「團員對帳單」。
* **重要屬性：** None
* **主要操作：** `generateShopSummary(roomId)`, `generateAuditList(roomId)`
* **協作者：** `OrderSession`, `OrderDetail`
* **來源/理由：** FR-04, FR-05 / 產出匯總報表。
