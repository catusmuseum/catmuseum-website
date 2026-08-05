---
title: Cat Museum 官網狀態
type: state
updated: 2026-07-31
---

# Website State

## 最終目錄結構
```
/
├── index.html              ← 首頁（永遠指向最近一場活動）
├── events/
│   ├── vol7/               ← Vol.7 台中場
│   │   ├── index.html      ← 活動主頁（含活動資訊＋相關頁面連結）
│   │   ├── visitor.html    ← 遊客須知（購票、流程、規範、通用規則）
│   │   ├── transport.html  ← 交通資訊
│   │   ├── exhibitors.html ← 參展名單
│   │   └── raffle.html     ← 抽獎贈品
│   └── _template/          ← 複製範本（開新活動用）
│       ├── index.html
│       ├── visitor.html
│       ├── transport.html
│       ├── exhibitors.html
│       └── raffle.html
├── vendor/
│   ├── index.html          ← 攤商專區入口
│   ├── rules.html          ← 攤商須知（固定規則）
│   ├── process.html        ← 報名流程（固定）
│   ├── faq.html            ← 攤商常見問題
│   └── vol7.html           ← Vol.7 報名資訊（費用、尺寸、期限）
├── about/
│   └── index.html          ← 關於我們（品牌故事＋聯絡資訊＋社群連結）
├── gallery/
│   └── index.html          ← 活動回顧（歷屆時間軸）
└── css/
    └── style.css           ← 共用樣式（含全域連結顏色設定）
```

## 導覽列（5 項）
首頁 | Vol.7 台中場 | 攤商專區 | 活動回顧 | 關於我們

## 開新活動流程
1. `cp -r events/_template/ events/vol8/`
2. 編輯 events/vol8/index.html（標題、日期、地點）
3. 編輯 events/vol8/visitor.html（票價、時程、場地配合事項、調整例外框）
4. 編輯 events/vol8/transport.html（交通路線）
5. 編輯 events/vol8/exhibitors.html（攤商名單）
6. 編輯 events/vol8/raffle.html（抽獎資訊）
7. 建立 vendor/vol8.html（報名資訊）
8. 在 vendor/index.html 新增卡片
9. 更新 index.html 指向新活動
10. **更新所有頁面導覽列**：將「Vol.7 台中場」改為「Vol.8 台北場」
    - 搜尋取代全部 18 個 HTML 檔案即可，約 2 分鐘

## 已完成
- 所有頁面遷移至新目錄結構
- 遊客須知已合併回活動子頁面（含活動資訊＋通用規範＋例外框）
- 導覽列 5 項固定連結，以當前活動為大標
- 活動總覽頁面移除（由活動回顧涵蓋歷史）
- 全域連結顏色已覆蓋（無預設藍色）
- events/_template/ 範本已建立