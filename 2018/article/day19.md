## Google Maps API Demo
---

### 網站功能之二 - OPEN DATA加上Google Maps API

Give me Find服務平台其中一項的功能是  
如果有遺失寵物的話，按照網頁流程輸入走失的日期，就會協助您有什麼事項需要注意。

其中這項功能是使用Google Maps API串連OPEN DATA製作而成的，今天來小小Demo一下
    
---

> 第一項是計算遺失寵物的天數，剛遺失寵物時為第0天，打開網頁會Google Maps取得當下位置，並畫出當下範圍方圓2公里的地方可供尋找範圍參考。

**在程式面是這樣寫的：**
先定位當下位置 → 增加Marker標記當下位置 → 在地圖畫圓

**使用的技術為：**
Maps JavaScript API 的 
[Geolocation](https://developers.google.com/maps/documentation/javascript/examples/map-geolocation) → [Marker](https://developers.google.com/maps/documentation/javascript/adding-a-google-map) → [Circles](https://developers.google.com/maps/documentation/javascript/examples/circle-simple)

![gif](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day19_1.gif?raw=true)   
    
---

> 第二項是計算遺失寵物的天數，剛遺失寵物時為1天時，打開網頁Google Maps取得當下位置，並串連opendata台北市動物醫院的資料集，找出各個醫院的經緯度標記在地圖上面。

**在程式面是這樣寫的：**
先定位當下位置 → 增加Marker標記當下位置 → 在地圖畫圓 → Ajax 呼叫 opendata api 回傳資料→ 遍歷經緯度Marker標記 

**使用的技術為：**
[Geolocation](https://developers.google.com/maps/documentation/javascript/examples/map-geolocation) → [Marker](https://developers.google.com/maps/documentation/javascript/adding-a-google-map) → [Circles](https://developers.google.com/maps/documentation/javascript/examples/circle-simple) → jQuery Ajax → [Marker](https://developers.google.com/maps/documentation/javascript/adding-a-google-map)
   
![gif](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day19_2.gif?raw=true)
    
---

> 第三項是計算遺失寵物的天數，剛遺失寵物時為2天以上時，打開網頁Google Maps取得當下位置，並串連opendata寵物登記站的資料集，找出各登記站的經緯度標記在地圖上面。

這邊的流程就和第二項一樣，就不多闡述了～
    
![gif](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day19_3.gif?raw=true)

因為今天又是星期六一整天都在自己整修住宅，又偷懶了...只做了Demo和大致講一下流程
之前有在Alex大大的直播節目中聊寫Google Maps API的想法和體檢code一下~
詳情請看：
影片 → [Alex宅幹嘛-你的 jQuery 我來 VUE 第二集：地圖應用](https://youtu.be/AkPmsTfPwUU)   
專案連結 → [GitHub-地圖應用](https://github.com/tinatyc/UrJqLetMeVue_GoogleMap)

**希望大家有什麼想知道的內容，歡迎在底下留言讓我知道，感激不盡！**


## 文後

---

越來越難想要寫什麼了....Orz（苦撐中...

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
