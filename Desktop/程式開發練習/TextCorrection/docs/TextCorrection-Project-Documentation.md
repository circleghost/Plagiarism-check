# TextCorrection 專案概述與執行方式

## 專案摘要

TextCorrection 是一個 macOS 應用程式，用於自動糾正與提升中文文本質量。它使用 OpenAI API 來分析並優化文本，特別關注繁體中文的語法、標點和格式。

### 主要功能

- 通過狀態欄圖標快速訪問
- 文本糾正與格式優化
- 顯示原文與修改後文本的比較 (高亮添加與刪除的內容)
- 基於 OpenAI API 的智能語言處理
- 熱鍵支持
- 用戶身份驗證 (Google 登入)

## 專案結構

專案採用 Swift 和 SwiftUI 開發，主要目錄結構如下：

```
TextCorrection/
├── TextCorrection/
│   ├── AppDelegate.swift        # 應用程式主要邏輯
│   ├── TextCorrectionApp.swift  # SwiftUI 主應用程式
│   ├── StatusItemManager.swift  # 狀態欄管理
│   ├── TextWindowManager.swift  # 文本視窗管理
│   ├── OpenAIService.swift      # OpenAI API 服務
│   ├── TextProcessing.swift     # 文本處理和比較邏輯
│   ├── SettingsWindow.swift     # 設定窗口
│   ├── HotKeyManager.swift      # 熱鍵管理
│   ├── PasteboardManager.swift  # 剪貼簿管理
│   └── Assets.xcassets/         # 圖片資源
├── TextCorrectionTests/         # 單元測試
└── TextCorrectionUITests/       # UI 測試
```

## 核心組件

### 1. AppDelegate (AppDelegate.swift)

主要應用程式委託類，負責：
- 初始化和協調所有服務和管理器
- 處理用戶身份驗證
- 管理文本處理邏輯
- 顯示和處理文本糾正視窗

### 2. StatusItemManager (StatusItemManager.swift)

管理 macOS 狀態欄的圖標，功能包括：
- 顯示應用程式狀態和菜單
- 提供快速訪問文本糾正功能
- 管理登入/登出選項

### 3. TextProcessing (TextProcessing.swift)

處理文本比較和差異顯示：
- 使用差異算法比較原始和修改後的文本
- 生成帶高亮的歸因字串，突顯添加和刪除的部分
- 自定義文本顯示樣式

### 4. OpenAIService (OpenAIService.swift)

與 OpenAI API 交互：
- 發送文本進行糾正
- 處理流式 API 響應
- 提供 API 密鑰驗證

### 5. TextWindowManager (TextWindowManager.swift)

管理文本顯示窗口：
- 創建和顯示浮動窗口
- 處理文本輸入和輸出
- 管理複製和關閉操作

## 應用程式流程

1. **初始化**：
   - 應用程式啟動並在狀態欄顯示圖標
   - 初始化所有管理器和服務
   - 檢查用戶身份驗證狀態

2. **用戶互動**：
   - 用戶點擊狀態欄圖標或使用熱鍵
   - 如未登入，顯示登入提示
   - 登入後，獲取選中文本或顯示文本輸入窗口

3. **文本處理**：
   - 獲取用戶輸入的文本
   - 通過 OpenAI API 發送請求
   - 接收 API 響應並逐步更新 UI

4. **結果顯示**：
   - 顯示原始文本和修改後的文本
   - 高亮顯示添加和刪除的內容
   - 提供複製結果選項

5. **設定與個性化**：
   - 通過偏好設定窗口自定義行為
   - 管理 API 密鑰和身份驗證
   - 配置熱鍵和其他選項

## 執行方式

### 開發環境

- macOS 14.0+
- Xcode 15.0+
- Swift 5.9+

### 執行步驟

1. **設置開發環境**：
   - 確保 Xcode 已安裝並更新
   - 安裝必要的依賴項（通過 Swift Package Manager）

2. **配置 API 密鑰**：
   - 獲取 OpenAI API 密鑰
   - 在應用程式中設置密鑰（通過設定窗口或鑰匙串）

3. **運行應用程式**：
   - 在 Xcode 中打開 TextCorrection.xcodeproj
   - 選擇目標裝置（macOS）
   - 點擊運行按鈕或使用 ⌘+R

### 使用方法

1. **基本使用**：
   - 點擊狀態欄圖標或使用預設熱鍵
   - 輸入或貼上要糾正的文本
   - 點擊"糾正"按鈕
   - 查看並可選擇性複製修改後的文本

2. **高級功能**：
   - 使用熱鍵直接處理選中的文本
   - 調整設定以自定義行為
   - 查看原始和修改後文本的詳細比較

## 技術細節

- **語言模型**：使用 GPT-4o-mini 進行文本處理
- **認證方式**：Google OAuth 登入
- **資料安全**：API 密鑰存儲在 macOS 鑰匙串中
- **主要依賴項**：
  - SwiftUI 用於 UI 構建
  - HotKey 用於熱鍵管理
  - KeychainAccess 用於安全儲存 API 密鑰
  - AuthenticationServices 用於身份驗證

## 系統需求

- macOS 14.0 或更高版本
- 互聯網連接（用於 API 請求）
- 有效的 OpenAI API 密鑰 