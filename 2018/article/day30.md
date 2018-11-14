## Facebook登入結合Firebase Authentication

_昨天把環境設定好之後已經去了半條命了...._
但是努力是有代價的，今天早上終於串成功啦～！！
來看看我怎麼弄的吧XD

### 使用ngrok建立https環境

今天我想想不要在花時間在SSL的設定上了，於是我選擇B方案：使用[ngrok](https://ngrok.com/)來當SSL的開發環境，照著官網的設定之後在要開啟的資料夾底下輸入，開啟連線。
```
./ngrok http 80
```
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_4.png?raw=true)

開啟網頁後居然有顯示錯誤！
「錯誤訊息：`Failed to complete tunnel connection`」

後來查到：[Failed to complete tunnel connection #478](https://github.com/inconshreveable/ngrok/issues/478)，解決方法是本地的server要一起開著，關關難過關關過啊....Orz

![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_3.png?raw=true)

### 使用fb登入結合firebase

根據上回([[day28]-雪恥戰！Firebase Authentication結合Facebook登入（上）](https://ithelp.ithome.com.tw/articles/10209531))在雙方的主控版設定好之後，接下來就是進行程式的撰寫。

- 引入Firebase SDK
在網頁的`body`裡引入相關Firebase的js
```
<!-- Firebase App is always required and must be first -->
<!-- Firebase App 這一隻js一定要掛在前面 -->
<script src="https://www.gstatic.com/firebasejs/5.5.8/firebase-app.js"></script>

<!-- Add additional services that you want to use -->
<!-- 其他看你要用到哪些功能，就選擇掛載哪隻js，這邊只用到auth&database -->
<script src="https://www.gstatic.com/firebasejs/5.5.8/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/5.5.8/firebase-database.js"></script>
```

- 接下來是將firebase初始化設定

```
<script type="text/javascript">

// Initialize Firebase
var config = {
    apiKey: "這邊填寫申請firebase api的key",
    authDomain: "你的服務名稱.firebaseapp.com",
    databaseURL: "https://你的服務名稱.firebaseio.com",
    projectId: "你的服務ID",
    storageBucket: "你的服務名稱.appspot.com",
    messagingSenderId: "產品的訊息id"
};
firebase.initializeApp(config); //啟動初始化

</script>
```
這邊設定檔不用擔心，firebase會自動幫你產生
1. 按下「 `+ 新增應用程式 `」
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_5.png?raw=true)

2. 選擇`web`平台
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_6.png?raw=true)

3. 直接產生firebase設定檔，直接貼在html裡即可
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_7.png?raw=true)

- 引入facebook初始化設定

```
/******** FB SDK載入 ********/
  window.fbAsyncInit = function() {
    FB.init({
      appId      : 'Facebook的應用程式編號',
      xfbml      : true,
      version    : 'v3.2'
    });
    FB.AppEvents.logPageView(); //
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
```

到這邊已經完成百分之87趴了....

接下來用Firebase的`new firebase.auth.FacebookAuthProvider();`呼叫FB Login並寫入至firebase裡

```
/******** FB Login ********/
//firebase 提供的functino-.auth.FacebookAuthProvider
var provider = new firebase.auth.FacebookAuthProvider();
firebase.auth().signInWithPopup(provider).then(function(result) {
  // This gives you a Facebook Access Token. You can use it to access the Facebook API.
  var token = result.credential.accessToken;
  // The signed-in user info.
  var user = result.user;
  var displayName = result.user.displayName;
  var email = result.user.email;

  console.log("msg");
  console.log(user);
  console.log(result);
  console.log(displayName);
  console.log(email)
  // ...
}).catch(function(error) {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  // The email of the user's account used.
  var email = error.email;
  // The firebase.auth.AuthCredential type that was used.
  var credential = error.credential;
  // ...
  console.log("msg2")
  console.log(error);
});

```
完成後會像這樣，進入網頁後會**彈跳出登入視窗**

![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_8.png?raw=true)

Demo演示，可以看到我輸入帳號之後會進行重新導向，資料會傳輸到Firebase，FB端則是驗證OK，回傳用戶資料出來～
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_1.gif?raw=true)

**到這邊終於完成我們Facebook登入結合Firebase Authentication了!!!**
我以為雪恥戰會失敗...因為中間實在遇到太多難題了，成就感十足啊～
   
---

### 2018年底 -

今年度的鐵人賽也到此結束了～

很開心今年可以和我的老師 - `Amos師父`還有推坑團教友 - `塔塔默`，一起組隊參加這次的鐵人賽（愛心～
真的很感謝他們兩位，我們常常在晚上10點收到提(ㄨㄟ)醒(ㄒ一ㄝˊ)通知信XD 
然後就很急著在LINE上面標注彼此的名字說「是誰還沒發文！！」，要不然就是「＠xxx ＠yyy 我今天鐵文囉～」XD

哈哈～這段歷程真的很開心，不像之前我獨自參加時那麼孤單、沒有動力....
這次也是我扎實的寫完鐵人賽，真的非常的開心～
今年也因為追大大們的直播，認識很多前端的朋友，大家一起互相交流，一起解決問題！
_PS:我在直播裡的小名是17(念e chi)，取自我名字英綺的諧音，平常在網路上可能叫做King或是King Tzeng。_
也很感謝這些直播的大大們辛勞，把我們前端人都拉在一起，比起兩年前我剛入行時，孤單一人沒人可以問問題，現在的前端生態真的好很多很多！

> Amos老師、Alex老師、Tommy老師，真心的感謝你們:)

感謝Amos老師的**阿摩斯的推坑教**裡的各方大大們，也感謝你們平日的解答～
最後還要感謝前端的朋友，互相交流切磋技術，在Alex同學見面會上認識的大家！感謝你們的鼓勵！

2018年底，鐵人賽落幕啦！！
最後我用這張gif圖來對我的師父也是我們團長致敬！謝謝各位～頒獎大會見了～～再見！！

*圖片提供者：[ 阿摩斯的推坑教 - 鐵 ]製作*
![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day30_2.gif?raw=true)
   
   
## 文後

---

要回歸正常的生活了...感動落淚TAT

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
