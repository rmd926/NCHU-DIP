# 數位影像處理作業（Colab 實作）

📎 **Colab 筆記本連結**：  
👉 [點此開啟程式](https://colab.research.google.com/drive/1bKqq6SFhWXPiMBJ0qGAFDKFEtO6qxrxi?usp=sharing)

> ⚠️ 所有程式碼整合於同一 Colab 筆記本中，依循題目流程撰寫，並未拆分為獨立小題模組。

---

## 📘 Q8. Median Filter 與胡椒鹽雜訊處理

### Q8-a. 實作 3×3 Median Filter
- 使用滑動視窗遍歷影像，每次取 3×3 區域進行排序，取中位數作為中心像素的新值。
- 處理後影像與原圖比較，可明顯觀察出對雜訊的抑制效果。

### Q8-b. 加入 Salt & Pepper 雜訊
- 定義雜訊參數：
  - `pa = pb = 0.1`
- 產生隨機矩陣：
  - 值 < `pa` → 設為 0（pepper）
  - 值 > `1 - pb` → 設為 255（salt）
- 將隨機雜訊套用於原圖產生具雜訊的圖像。

### Q8-c. Median Filter 對比分析
- 對比下列兩種方式的輸出結果：
  1. 原圖 ➜ Median Filter
  2. 原圖 ➜ Salt & Pepper ➜ Median Filter
- 可見 median filter 對於雜訊的濾除能力尤其對 salt & pepper 雜訊有顯著改善。

---

## 🧭 Q9. 頻域陷波濾波（Notch Filter）

- 對影像疊加合成一組正弦波噪音。
- 對影像進行傅立葉變換（`np.fft.fft2`）並中心化（`np.fft.fftshift`）。
- 根據噪音頻率設計陷波濾波器（Notch Mask），將對應頻率位置設為 0，其餘為 1。
- 將原始頻域圖像乘上 Mask，以去除指定頻率。
- 最後進行反傅立葉轉換（`np.fft.ifft2`）還原空間域圖像，觀察噪音抑制效果。

---

## 🌀 Q10. 運動模糊 + 高斯雜訊 + 維納濾波還原

### 模糊處理
- 根據課本 5.6-11 式子模擬 +45 度向上的 motion blur。
- 模糊函數參數：
  - `a = 0.1`, `b = 0.1`, `T = 1`

### 雜訊加入
- 對模糊後圖像加入 **高斯雜訊**，方差為 `10`。

### 頻域復原（Wiener Filtering）
- 將模糊＋雜訊影像進行傅立葉變換與中心化。
- 建立 Wiener Filter：
  - 預設使用高斯型的 PSF 預估
  - 搭配雜訊與模糊估計，自動平衡還原與雜訊放大問題
- 最後將結果反變換回空間域得到復原圖像，明顯提升清晰度與細節。

---

## 🛠 使用技術與工具

- Python 3.x
- NumPy (`np.fft`, `np.random`)
- OpenCV (`cv2`)
- Matplotlib (`pyplot`)
- Google Colab 環境執行與視覺化

---

## 📌 備註

- 各題目所使用的參數皆可調整以進行進一步實驗（如雜訊比例、模糊強度、濾波器大小）。
- 所有圖片結果皆於 Colab 即時呈現，便於分析不同處理效果之優劣。
