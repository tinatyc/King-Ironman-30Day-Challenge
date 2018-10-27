## 網站核心功能 - WebRTC
---


Give me Find服務平台主打的項目之一就是不用下載app，
直接瀏覽網頁按照引導流程就能找到浪浪的身分、主人等等～

其中一個關鍵的技術就是使用網頁開啟相機掃描QRCode
找到了國外開發者開發的github專案(https://github.com/schmich/instascan )，拿來加以修改。

這大概是一年前初次測試的時候錄的Demo影片
![Yes](https://youtu.be/33nOeskNdhc)
PS:這是我在家的宅樣XD

這是用電腦的webcam試做，
程式流程是開啟相機 → 掃描QRCode → 掃到QRCode的文字後去用字串去資料庫抓資料→顯示在前端

當然用手機也是可以開的，只是因為現在iOS支援度上時好時壞，之前看到iOS 11要支援WebRTC了，但是實測開啟相機的警示有跳出了，鏡頭還是沒開啟，這部份我必須要在debug一下....
之前有位邦友剛好有這個問題-[網頁啟動鏡頭掃描QRcode](https://ithelp.ithome.com.tw/questions/10187814)，可以看看我們的討論串～

Demo是用Android的手機開啟我做的網頁，開啟後掃描QRcode，我在功能上修改了可以切換前置鏡頭和後置鏡頭，以防手機型號的不同，認到的鏡頭也不大一樣。
![Yes](https://youtu.be/yz9waxJZ7nU)

因為今天是星期六稍微喘息一下，有點偷懶只做了Demo展示，
明天可能會推薦我現在在用的Chrome套件（因為有人許願～

**希望大家有什麼想知道的內容，歡迎在底下留言讓我知道，感激不盡！**

## 文後

---

這兩天因為某件事情傷神傷身，結果被搞了一頓心情不太好.....    
前端朋友們、大大們跑來安慰我，我真的心裡很感動，謝謝你們TAT

---

### 團隊主題連結

> CssCoke - **Amos 老師**
>
> - 影片教學組- **[金魚都能懂的網頁設計入門 - 金魚都能懂了你還怕學不會嗎](https://ithelp.ithome.com.tw/users/20112550/ironman/2072)**
> - Modern Web- **[連續 30 天的超實務網頁設計的垂直置中教學](https://ithelp.ithome.com.tw/users/20112550/ironman/2092)**

> 塔塔默
>
> - Modern Web- **[使用 Leaflet 及 Folium 開啟網頁地圖大門](https://ithelp.ithome.com.tw/users/20112552/ironman/2074)**

---
