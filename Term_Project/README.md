# 🎨 色彩轉換與直方圖匹配實作說明（Colab 環境）

📎 **Colab 筆記本連結**：  
👉 [點此開啟程式](https://colab.research.google.com/drive/1KXSbGV0q83nXd9x5HNciQ3GaF7by5UBE?usp=sharing)

> 本程式實作色彩轉換與直方圖匹配相關操作，並輔以視覺化對照，涵蓋 Lab 色彩空間轉換、直方圖平滑、區域對比調整等技術。亦支援使用者調整轉移比例與模糊核大小以進行分析。

---

## 📌 Figure 5：色彩轉移流程（Lab 空間）

- **色彩空間轉換**：  
  使用 `rgb_to_lab` 及 `lab_to_rgb` 將影像在 RGB 與 Lab 色彩空間間來回轉換。

- **直方圖計算與平滑**：  
  使用 `compute_histogram` 計算 Lab 各通道的直方圖，並利用 `smooth_histogram` 搭配高斯濾波器進行平滑，減少雜訊干擾。

- **局部最小值檢測與區域切割**：  
  使用 `detect_minima` 找出平滑直方圖中的局部極小值，用於切分色彩區段，提升顏色重塑精度。

- **區域重塑與顏色轉移**：  
  透過 `reshape_histogram_region` 進行統計對齊，再用 `transfer_color` 完成 Lab 值的區域轉換，實現兩圖間色彩轉移。

---

## 🐯 Figure 7：遮罩式區域轉換應用

- **第一部分**：將整張 target image 的顏色轉移至 source image，產生紅底效果。
- **第二部分**：僅將老虎以外的綠色草皮應用 target 顏色，藉由遮罩保留老虎原色，達到局部顏色替換的效果。

---

## 📊 Figure 9：直方圖匹配與平滑化

- **直方圖計算與高斯平滑**：  
  使用 `compute_histogram` 與 `smooth_histogram` 處理各通道直方圖。

- **核心轉換邏輯 `match_histograms`**：  
  1. 計算 source 與 target 各通道直方圖與累積分佈函數 (CDF)
  2. 建立查找表並進行像素值映射
  3. 可透過 `match_percent` 調整轉移比例以控制轉換強度

---

## 📈 Figure 10：不同轉移比例比較

- 延伸 Figure 9 的流程，分別以 `15%`、`25%`、`50%` 進行顏色轉移並視覺化，展示轉移強度對結果的影響。

---

## 🎨 Figure 14~16：完整 Lab 通道匹配與對比調整

- **Lab 通道匹配**：  
  對 L*、a*、b* 各通道執行 `match_histograms`，以對齊整體色彩分佈，並允許設定 `transfer_ratio`（0~1）控制轉移強度。

- **局部對比調整**：  
  使用 `adjust_local_contrast` 對 Lab 中的 L* 通道進行強化：
  1. 提取源圖與轉換圖之 L 通道
  2. 高斯模糊產生細節層差異
  3. 對應調整後融合回 L 通道
  4. 確保調整後仍落於合法範圍

- **色調曲線視覺化**：  
  使用 `plot_tone_curve` 比較轉換前後 L 通道 CDF，觀察轉移對色調的影響，並支援自訂 transfer ratio 參數。

---

## ✨ 額外實作：不同高斯模糊核大小對細節的影響

- 提供 `3x3` 與 `7x7` 兩種模糊核選項：
  - **3x3**：細節保留多，處理精確。
  - **7x7**：畫面柔化程度更高，但可能犧牲部分邊緣銳度。

---

## 🛠 使用技術與套件

- Python 3.x
- NumPy
- OpenCV
- SciPy
- Matplotlib
- Google Colab

---

## 📎 備註

- 所有功能模組化，可自由調整參數（如匹配強度、遮罩區域、模糊核大小）。
- 建議結合原圖與轉換圖像進行比對分析，以深入理解色彩統計重構流程。
