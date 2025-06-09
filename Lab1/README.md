# 數位影像處理作業說明（Colab 環境）

> 📌 [點此開啟 Colab 筆記本](https://colab.research.google.com/drive/1jEN7bJCFt8Q9pp5POcDGxrY6NSRclQl_?usp=sharing)

本次作業於 Google Colab 環境完成，並使用 `matplotlib.pyplot` 進行視覺化繪圖與結果展示。以下針對 Q8～Q10 題目說明程式邏輯與處理方式。

---

## 📘 Q8. 影像強度重新量化（Intensity Re-quantization）

### a) 將圖像強度從 256 降為 2 個灰階級距  
- 圖像讀入後，先顯示原圖。
- 接著利用「取模」方式將圖像灰階重新量化為 2 級，做簡化處理。
- `new_img = (img / (256 / level)).astype(int) * (256 / level)`。

### b) 批次顯示不同的量化等級（16, 8, 4, 2）
- 修改程式讓 `desired_level` 接受陣列 `[16, 8, 4, 2]`。
- 透過迴圈依序處理並顯示所有 re-quantized 結果。
- 圖像排列為每列兩張，模仿課本呈現格式。

---

## 🔍 Q9. Zoom & Shrink（影像放大與縮小）

### a) 製作 Zoom 與 Shrink 函數並視覺化
- 分別撰寫 `zoom()` 與 `shrink()` 函數。
- 使用放大與縮小倍率處理後，將圖 resize 成原圖尺寸以利比較。
- 最終顯示三張圖：原圖、放大圖、縮小圖。

### b) 將圖像縮小 12 倍並儲存
- 套用 `shrink()` 函數縮小倍率設為 12。
- 將結果以 `cv2.imwrite()` 或 `plt.imsave()` 儲存以供後續使用。

### c) 將縮小後影像再放大 12 倍以進行比較
- 讀取前一步儲存的圖。
- 使用 `zoom()` 函數還原至原始尺寸進行視覺化比較。

---

## 🌀 Q10. 仿射轉換（Affine Transformation）

### a) 調整旋轉角度、裁切比例與平移距離
- 使用 `lena` 圖作為初始圖像。
- 將圖像：
  - 旋轉 23 度、
  - 平移 x:18、y:22 像素、
  - 裁切比例設為 2/3。
- 對應函數可使用 OpenCV 中的 `getRotationMatrix2D` 與 `warpAffine`。

### b) 改用指定圖片並實作三種內插法
- 套用相同轉換步驟至指定圖像。
- 分別使用 OpenCV 提供的三種內插方式實作：
  - 最近鄰插值（`cv2.INTER_NEAREST`）
  - 雙線性插值（`cv2.INTER_LINEAR`）
  - 立方插值（`cv2.INTER_CUBIC`）

---

## 🛠 使用套件

- Python 3.x
- OpenCV (`cv2`)
- NumPy
- Matplotlib (`pyplot`)
- Colab 環境內建支援

---

📎 **備註**  
作業程式已全數整合於 Google Colab 筆記本，並可直接於瀏覽器中執行及展示結果。
