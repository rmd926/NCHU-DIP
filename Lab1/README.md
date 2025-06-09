本人在本次作業使用colab環境進行撰寫，故使用matplotlib裡面的pyplot去作圖。
Q8:
a)因為間隔數量=256去 mod level，所以將圖像讀進來之後，分別呈現原圖以及將強度從256變為2的圖。

b)這題就是把原本的desired_level從int換成輸入一個陣列，唯一要改變的就是最後寫一個迴圈去跑陣列中的所有數字，也就是16,8,4,2，並且效仿課本一樣一行出現兩張圖。


Q9:
a)就是寫兩個function分別是zoom和shrunk，就是把圖片*zoom或shrink的倍數之後，再把圖片resize。那圖片呈現的分別是原圖、zoom、shrunk。

b)這題就是保留a)程式碼中shrink function，然後調成12倍再把圖畫出來，並存起來備用。

c)本人把b)存出來的圖再用zoom 12倍回去進行比較。


Q10
a)本題主要考量的是旋轉角度、裁切的比例、還有translate的pixel，那本人是使用lena作為實驗圖。
b)分別把圖片旋轉23度，x y shift 18 、 22個pixel，並且把裁切比例調成2/3，基本上做完上述步驟再把圖片換成指定圖即可。
接著再參考課本的三種內插法進行實現，那這部分也挺簡單，因為cv2有內建的套件，直接套完再作圖就可以了。


本次作業colab連結在此:
https://colab.research.google.com/drive/1jEN7bJCFt8Q9pp5POcDGxrY6NSRclQl_?usp=sharing
