### 一、生理數據偵測（PPG影像量測）
#### 循序圖（Sequence Diagram）
```mermaid
sequenceDiagram
    participant User as 使用者
    participant Mirror as 智慧鏡面系統
    participant Camera as 鏡頭模組
    participant PPG as PPG演算法
    participant Cloud as 雲端資料庫

    User ->> Mirror: 站在鏡面前
    Mirror ->> Camera: 啟動鏡頭
    Camera ->> PPG: 傳送影像資料
    PPG ->> Mirror: 回傳心率、血氧結果
    Mirror ->> User: 顯示即時量測結果
    Mirror ->> Cloud: 上傳量測數據
    alt 光線不足或晃動
        Mirror ->> User: 顯示重新量測提示
    end
```
#### 活動圖（Activity Diagram）
```mermaid
flowchart TD
    A[使用者站於鏡前] --> B[啟動鏡頭與PPG演算法]
    B --> C[分析臉部血流變化]
    C --> D[顯示量測結果於鏡面]
    D --> E[暫存並上傳至雲端]
    E --> F{光線不足或使用者晃動?}
    F -->|是| G[提示重新量測]
    F -->|否| H[結束]
    G --> B
```
### 二、健康分析與建議（AI + LLM）
#### 循序圖（Sequence Diagram)
```mermaid
sequenceDiagram
    participant Mirror as 智慧鏡面系統
    participant AI as AI健康分析模型
    participant LLM as LLM模組
    participant Chatbot as LINE Chatbot
    participant Cloud as 雲端資料庫

    Mirror ->> AI: 傳送量測結果
    AI ->> LLM: 傳送分析結果
    LLM ->> Mirror: 回傳健康報告與建議
    Mirror ->> Chatbot: 同步發送健康建議
    Mirror ->> Cloud: 儲存健康報告
    alt 資料缺失或異常
        Mirror ->> User: 顯示分析中斷訊息
    end
```
#### 活動圖（Activity Diagram）
```mermaid
flowchart TD
    A[開始分析] --> B[取得量測結果]
    B --> C[AI模型進行數據分析]
    C --> D[LLM生成健康報告與建議]
    D --> E[鏡面與LINE同步顯示]
    E --> F[儲存報告於雲端]
    F --> G{資料是否完整?}
    G -->|否| H[顯示分析中斷]
    G -->|是| I[分析完成]
    H --> I
```
### 三、異常警示與通知
#### 循序圖（Sequence Diagram)
```mermaid
sequenceDiagram
    participant System as 智慧鏡面系統
    participant User as 使用者
    participant Family as 家屬
    participant Chatbot as LINE Chatbot
    participant Cloud as 資料庫

    System ->> System: 偵測健康數據異常
    System ->> User: 顯示紅色警示訊息
    System ->> Chatbot: 傳送異常通知
    Chatbot ->> Family: 發送通知訊息
    Family ->> Chatbot: 點擊查看詳細報告
    Chatbot ->> Cloud: 讀取健康報告資料
    alt LINE服務中斷
        System ->> User: 僅顯示鏡面警示
        System ->> Cloud: 暫存異常事件
    end
```
#### 活動圖（Activity Diagram）
```mermaid
flowchart TD
    A[開始監測健康數據] --> B[偵測是否異常]
    B -->|是| C[顯示紅色警示]
    C --> D[發送LINE通知]
    D --> E[家屬查看詳細報告]
    B -->|否| F[持續監測]
    D --> G{LINE服務是否正常?}
    G -->|否| H[僅顯示鏡面警示並暫存]
    G -->|是| I[完成通知程序]
    H --> I
```
