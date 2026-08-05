# 攤位名單 Google Sheets 同步 — 設定說明

## 目標
更新 Google Sheets → 網站自動更新，不需修改 HTML。

## 資料流
```
原始攤位分頁 → Website_Data 分頁 → 發佈到網路(CSV)
                                         │
                    ┌────────────────────┘
                    ▼
        雙層讀取策略（exhibitors.html）：
            1. 先試本機 exhibitors.json（無 CORS 問題）
            2. 失敗則 fallback 到 Google CSV 公開網址
```

## 已完成
- ✅ `Website_Data` 分頁已發佈到網路（CSV 格式，公開免登入）
- ✅ `events/vol7/exhibitors.html` 雙層讀取：JSON → fallback CSV
  - 商業攤位顯示特色卡片（含品牌介紹）
  - 全部攤位（商業+一般）顯示在一個清單
  - 品牌連結不在此頁顯示（僅贊助攤位在抽獎專區有連結）
- ✅ 自動同步腳本 `sync_exhibitors.py`（每 30 分鐘更新 exhibitors.json）

## 同步腳本
- 位置：`~/AppData/Local/hermes/scripts/sync_exhibitors.py`
- 功能：抓取 Google CSV → 轉換為 JSON → 寫入 `events/vol7/exhibitors.json`
- 排程：每 30 分鐘自動執行（cron job: 82879074e3b1）
- 手動執行：`cd ~/AppData/Local/hermes/scripts && python sync_exhibitors.py`

## 日常維護（非工程師也能做）
- **新增/移除攤位**：直接編輯原始分頁 → 網站自動更新（CSV 即時，JSON 最多 30 分鐘同步）
- **商業攤品牌介紹**：在 Website_Data 的「品牌介紹」/「Facebook」/「Instagram」/「Plurk」欄填寫 → 網站自動更新
- **調整顯示順序**：在「排序」欄填數字（小到大）

## 注意事項
- 發佈到網路只暴露 Website_Data 分頁，其他分頁安全
- 本機開啟 file:// 時用 JSON（無 CORS），上線後用 CSV（即時更新）
- 如果有人看到資料沒更新，重新整理頁面即可

## 擴充（未來）
- 其他活動 Vol.8：複製 `events/_template/exhibitors.html`，改 CSV_URL 和 JSON_URL

## 疑難排解
| 問題 | 解決 |
|------|------|
| 網站顯示「無法載入攤位名單」 | 檢查 CSV_URL 或 JSON 是否正確 |
| 本機打開看不到名單 | 先執行 `python sync_exhibitors.py` 產生 JSON |
| 資料更新後網站沒變 | 重新整理頁面，或等 30 分鐘內同步 |