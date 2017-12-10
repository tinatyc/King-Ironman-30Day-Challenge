## 結果假日天氣變好冷...頭痛荒廢了兩天...
長期用電腦的我們肩頸那邊的筋很僵硬，天氣突然變冷了連帶也會造成腦部疼痛...![/images/emoticon/emoticon06.gif](/images/emoticon/emoticon06.gif)
記得要保暖好頭部和頸部，程式開發者辛苦了TAT (敬禮

---

抱歉星期六也就是昨天天氣變化太大身體不適，也就先卡文了...
昨天的文就改寫[peter0521](/users/20066990)網友留言點播的**Google Calendar API** Sample練習好了...
因為我都是當日寫的沒有庫存文章...
擇日補上，非常抱歉...![/images/emoticon/emoticon02.gif](/images/emoticon/emoticon02.gif)
**今天緩一下來做地圖定位這塊的撰寫好了**

---
> #### 起始式

**Google Marker的應用尚未結束，還有很多Event沒有解說，請搬板凳慢慢等待...**(被打![/images/emoticon/emoticon05.gif](/images/emoticon/emoticon05.gif)
大家用Google Map最常的動作"**之一**"，應該有定位`目前的位置`這個功能吧～

定位目前位置可以作很多的應用，舉凡`購物時可以找尋你家附近的分店`、或是你`迷路時打開目前定位導航`等....
那就不多說，附上參考資料
> Maps JavaScript API - [Geolocation](https://developers.google.com/maps/documentation/javascript/examples/map-geolocation)

其實定位非常的簡單，原理是：

#### **獲取設備當前的位置 -> 取得經緯度 -> 傳給Google Maps API**

這箇中的奧妙就在`獲取設備當前的位置`是用`Javascript提供的Web API`來取得經緯度，而不是用Google提供的API來取得經緯度！
![https://ithelp.ithome.com.tw/upload/images/20171210/20103130VIbf25gO7e.png](https://ithelp.ithome.com.tw/upload/images/20171210/20103130VIbf25gO7e.png)
> 參考資料 - MDN開發者技術文件 [Geolocation](https://developer.mozilla.org/zh-TW/docs/Web/API/Geolocation/getCurrentPosition)

解析一下Google的Sample
![https://ithelp.ithome.com.tw/upload/images/20171210/20103130NvmGrocxoQ.png](https://ithelp.ithome.com.tw/upload/images/20171210/20103130NvmGrocxoQ.png)

`navigator.geolocation`會回傳一個 Geolocation 物件，透過這個物件可以存取Device的位置資訊。
**但是因為有隱私的因素在，會先詢問User是否允許授權！**（重要）

> **[ 這邊有我今年自己的做的side project來做截圖範例 ]**
跳"是否允許授權"↓
![https://ithelp.ithome.com.tw/upload/images/20171210/20103130bg20fp2H9a.png](https://ithelp.ithome.com.tw/upload/images/20171210/20103130bg20fp2H9a.png)

> 允許授權後↓
![https://ithelp.ithome.com.tw/upload/images/20171210/201031308a9C0ljEto.png](https://ithelp.ithome.com.tw/upload/images/20171210/201031308a9C0ljEto.png)

大致上該注意的就這些了～（欸？就醬？

---

> 練習Time

所以練習寫顯示目前位置的地圖~

```
<!DOCTYPE html>
<html lang="zh-tw">

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>King Tzeng的鐵人地圖</title>
    <style type="text/css" media="screen">
    html {
        height: 100%;
        width: 100%;
        background-image: linear-gradient(45deg, #ff9a9e 0%, #fad0c4 99%, #fad0c4 100%);
    }

    #map {
        position: absolute;
        left: 0;
        height: 80%;
        width: 100vw;
    }

    #body {
        height: 100%;
        width: 100vw;
        position: relative;
        top: 0;
        left: 0;
    }

    h1,
    h2 {
        text-align: center;
    }

    h2 {
        width: 100%;
        background-color: rgba(255, 255, 255, 0.45);
    }
    </style>
</head>

<body>
    <div class="body">
        <h1>King Tzeng的鐵人地圖</h1>
        <h2>抓取當前位置的練習</h2>
        <div id="map"></div>
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script>
    function initMap() {
        var latlng = { lat: 25.046891, lng: 121.516602 }; // 給一個初始位置
        var map = new google.maps.Map(document.getElementById('map'), {
            zoom: 14, //放大的倍率
            center: latlng //初始化的地圖中心位置
        });
        var marker = new google.maps.Marker({
            position: latlng,
            map: map
        });
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(function(position) {
                var pos = {
                    lat: position.coords.latitude,
                    lng: position.coords.longitude
                };
                var marker = new google.maps.Marker({
                    position: pos,
                    icon:'marker.png',
                    map: map
                });
                map.setZoom(17);
                map.setCenter(pos);
            });
        } else {
            // Browser doesn't support Geolocation
            alert("未允許或遭遇錯誤！");
        }
    } //init_end
    </script>
    <script async defer src="https://maps.googleapis.com/maps/api/js?key=AIzaSyC_Za7RqKvUuEg2Nln0EcpUVN3k2fZtDuE&callback=initMap">
    </script>
</body>

</html>


```
