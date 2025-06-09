# 數位影像處理作業說明（Colab 實作）

📎 **Colab 連結**：  
👉 [點此開啟 Colab 筆記本](https://colab.research.google.com/drive/1L5XuxbpgwSap7UzPJkeRakphqRjNG1Sp?usp=sharing)

> ⚠️ 本次題目彼此環環相扣，因此所有小題的程式碼皆整合撰寫，並未進行區段分離。

---

## 📘 Q8. 直方圖與均衡化（Histogram & Equalization）

### 8-a. 原始圖像的直方圖繪製
- 使用 `OpenCV` 的 `cv2.calcHist` 函數計算圖像灰階直方圖。
- 灰階範圍設定為 `[0, 255]`，並使用 matplotlib 進行視覺化。

### 8-b. 累積分布函數（CDF）與映射
- 透過 `histogram.cumsum()` 計算直方圖的 CDF。
- 建立一個對應的強度映射函數，將原圖像像素對應至 CDF，為後續均衡化作準備。

### 8-c. 圖像均衡化與視覺化
- 載入原圖，分別套用 8-a 與 8-b 的處理函式。
- 將原圖與均衡後圖像以及其對應的直方圖一同顯示。
- 可觀察原圖像像素值多集中於 0 附近，而均衡化後則明顯擴展至中間灰階（約 128）附近。

---

## 🔍 Q9. Laplacian 增強與遮罩設計

### 9-a. 自訂 Laplacian 遮罩進行空間濾波
- 定義 `spatial_filtering()` 函式。
- 使用者可自訂 3x3 的 Laplacian Mask，並透過雙層 for-loop 進行濾波運算。
- 可自由替換遮罩參數進行濾波效果實驗。

### 9-b. Laplacian 增強操作
- 定義 `laplacian_enhancement()` 函式。
- 套用使用者定義的 Laplacian 遮罩於原圖上，並返回增強後圖像。
- 增強方式為加權合成原圖與遮罩結果，提升邊緣銳利度。

### 9-c. 多張圖像套用 Laplacian 增強
- 將 3-38 範例中的所有圖依序進行 Laplacian 增強處理。
- 結果統一顯示，用以觀察不同圖像套用同一遮罩的表現差異。

---

## 🌀 Q10. 高增幅濾波（High-boost Filtering）

### 10-a. 改良版 Laplacian Mask 實作
- 延續 Q9-a 的 `spatial_filtering()`，加入 `mask_sum` 計算遮罩總和以提升通用性。
- 解決原本寫死遮罩值的限制，使得程式更具彈性。

### 10-b. 高增幅濾波應用與實驗結果
- 將模糊影像（經平均濾波處理）當作平滑版本 `f̄(x,y)`。
- 採用課本中建議的參數 `k = 4.5` 作為高增幅濾波器權重。
- 結果顯示：圖像邊緣（如文字）變得更清晰，但也會出現些許銳化過度導致的裂痕或雜訊。

---

## 🛠 使用套件

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- Matplotlib (`pyplot`)
- Google Colab 環境執行與視覺化

---

📌 **備註**：  
所有程式碼與結果整合於同一份 Colab 筆記本中，可即時修改、執行與預覽處理流程與視覺結果。
