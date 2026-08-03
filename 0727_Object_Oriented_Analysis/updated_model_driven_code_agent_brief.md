
# 更新後之模型驅動實作任務書

### 任務名稱：`main.py` 物件導向重構與狀態鎖定保護強化

1. **重構目標：** 將原本混在 FastAPI 路由函式內的點餐與計價邏輯，抽離至獨立之 `OrderSession` 與 `PricingService` 類別，落實 BCE 責任分離。
2. **狀態保護規則：** `OrderSession` 物件內部維護 `is_closed` 布林值，任何修改點單之請求必須呼叫 `session.can_accept_orders()`。若回傳 `False`，後端路由強制拋出 `HTTP 403 Forbidden`。
3. **完成標準：** 重構後全數通過主要流程測試（TC-M-01~05）與鎖單攔截測試（TC-E-01），且不改變任何原有 API 介面合約。
