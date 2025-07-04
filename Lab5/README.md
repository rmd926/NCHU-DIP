# 數位影像處理作業說明（Colab 實作）

📎 **程式筆記本連結**：  
👉 *https://colab.research.google.com/drive/1M11jAaIqpvMGRrZG16LFGnCvID_VT2Zu?usp=sharing*

> ⚠️ 本次作業於 Google Colab 環境開發完成，程式碼整合執行並依據題目邏輯順序排列。

---

## 🎨 Q8. Pseudo-color 偽彩色轉換

- 本題將灰階影像依不同灰階值範圍映射為彩色圖像。
- 根據灰階值（`gray_level`）進行條件式轉換：
  1. **0 ≤ gray < 64**  
     `R = 0`，`G = gray × 4`，`B = 256`
  2. **64 ≤ gray < 128**  
     `R = 0`，`G = 256`，`B = 128 - (gray × 4)`
  3. **128 ≤ gray < 192**  
     `R = (gray × 4) - 512`，`G = 256`，`B = 0`
  4. **192 ≤ gray < 256**  
     `R = 256`，`G = 1024 - (gray × 4)`，`B = 0`
- 所有 RGB 值最後正規化至 `[0, 1]` 以便使用 `matplotlib` 顯示。

---

## 🌈 Q9. RGB ↔ HSI 轉換與直方圖均衡化

- 撰寫兩個函數：
  - `rgb_to_hsi(R, G, B)`
  - `hsi_to_rgb(H, S, I)`
- 實作完全依據課本公式處理三個通道的轉換，考慮角度、強度與飽和度處理細節。
- 將原始 RGB 圖像分離為三個 channel。
- 對每個 channel 分別執行直方圖均衡化（使用 `cv2.equalizeHist()`）。
- 將均衡化後的 R, G, B 通道合併為最終彩色圖像。

---

## 🧪 Q10. R 通道特徵區域選擇與 Mask 篩選

- 從 R 通道中擷取一個區域：
  - 行索引：`128 ~ 255`
  - 列索引：`85 ~ 169`
- 計算該區塊的統計資訊：
  - 平均值 `R1_ave`
  - 標準差 `R1_d`
- 設定強度範圍作為條件篩選 mask：
  ```python
  mask = (R > R1_ave - 1.25 * R1_d) & (R < R1_ave + 1.25 * R1_d)
最終將符合條件之像素設為 1，其餘為 0，產生二值化遮罩影像進行顯示。

🛠 使用工具與環境
Python 3.x

NumPy

OpenCV (cv2)

Matplotlib (pyplot)

Google Colab 平台

📌 備註
所有轉換與篩選邏輯皆可參數化修改，便於進一步進行測試與應用。

建議搭配原圖與結果圖並列展示，以利分析處理前後差異。

RGB ↔ HSI 的轉換運算請特別注意角度單位（度／弧度）與範圍正規化。



