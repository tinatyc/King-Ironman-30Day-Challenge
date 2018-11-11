## firebase Authentication Demo
---

### 新篇章

由於我在商業化驗證檢核沒有過關被刷下來了，最後一個商業化募資階段就沒有內容可以寫了....
不過這個side project還是會持續做下去，就和此系列文的主題引言說的
>2017 年 - 為了證明自己的實力，我參加了經濟部工業局所舉辦的「資料創新應用競賽」，並以平日工作休息之餘做出 Side Project：『Give me Find (幫我找)-促進寵物福利協尋平台』獲得 複選優等；
2018 年 - 心中推廣動物福利的夢還未完成！就趁這個機會把網站重構，審視有哪些地方可以改進，並紀錄與分享參賽歷程。

**在比賽階段沒做好的地方，現在開始慢慢完成...**
   
   
### firebase Authentication

今天要小小Demo的是`firebase Authentication`
說實在因為我不是本科系出身的，對於後端資料庫的部分不是很了解....
但是網站又要規劃會員服務需要資料庫來的support，後來找到了[firebase](https://firebase.google.com/)這個服務，大大的舒緩了前端不會後端的困境啊....

為了要實現會員的這個功能，去年有小小研究一下Firebase，有實現出
- 使用FaceBook註冊、登入
- 使用Google帳號註冊、登入
- 使用自己的mail註冊、登入

以上的功能，但是就在寫文章的剛剛我發現到一件事情.....


`就是我太久沒進去Facebook的開發應用那邊，隱私權政策改了沒有申請被撤除權限了T口T`
還有剛剛firebase也是太久沒有用，登進去整個也改版了....Orz(悲劇)

現在只剩下`使用自己的mail註冊、登入`可以Demo給大家看了.....

那個不多說了...就放影片Demo一下 Give me Find網站的新功能

> firebase Authentication 
註冊Demo
[![Yes](https://img.youtube.com/vi/_raRqbDVT-8/0.jpg)](https://www.youtube.com/watch?v=_raRqbDVT-8)

> firebase Authentication 
登入Demo
[![Yes](https://img.youtube.com/vi/https://youtu.be/vtydHGupTjM/0.jpg)](https://www.youtube.com/watch?v=https://youtu.be/vtydHGupTjM)

---
### 串Firebase API 的隨手筆記

這個是去年(2017年)我在部落格發表的隨手筆記，現在有可能api改了，僅供參考
連結：[King 學習前端之人生-〔筆記〕串Firebase API 之隨手筆記](https://kingweblife.blogspot.com/2017/10/firebase-api.html)

```
API名稱：onAuthStateChanged
用法：登入後的狀態
範例：

login_btn.addEventListener("click",function(){
  console.log(acc_user_L.value);
  firebase.auth().signInWithEmailAndPassword(acc_user_L.value, psw_user_L.value).catch(function(error) {
    // Handle Errors here.
    console.log(error);
    var errorCode = error.code;
    var errorMessage = error.message;
    console.log(errorMessage);
  })
  firebase.auth().onAuthStateChanged(function(user) {
    console.log(user);    //這裡會印出User的資訊
    if (user) {
      // User is signed in.
    }
  });
},false);
```

![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day26_1.png?raw=true)
    
> 這個API怎麼用勒？

```
firebase.auth().onAuthStateChanged(function(user) {←//這邊帳號登入後，登入的狀態產生變化
    console.log(user);
//上圖的firebase.UserInfo#displayName的"UserInfo"就是指function(user){}函式裡的user
//所以官方文件裡就寫firebase.UserInfo可以取User的XXX，指的是配合大函式回傳的東西
    if (user) {
      // User is signed in.
      console.log(user.uid);
      console.log(user.providerId); 
      // console.log(user.email);
      // displayName
      // emailVerified
      // phoneNumber
      // photoURL
      // providerData
    }
  });
},false);
```

![img](https://github.com/tinatyc/King-Ironman-30Day-Challenge/blob/master/2018/article/img/day26_2.png?raw=true)
   
    
今天週六夜先寫到這邊了....Orz

**希望大家有什麼想知道的內容，歡迎在底下留言讓我知道，感激不盡！**    
    

## 文後

---

該學的逃不掉，公司叫我用PHP去寫前後端，現在後端也要慢慢碰一點了....
其實我不是完全不會後端語言啦...只是PHP連接資料庫那一部分不會罷了Orz

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
