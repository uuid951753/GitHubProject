#NodeJs 練習創建自己的專案<br />
&nbsp; &nbsp;聊天室頁面不能刷新 刷新會斷開連接 考慮解決方法<br />
&nbsp; &nbsp;聊天室中能保存100條信息<br />
&nbsp; &nbsp;本聊天室基於NodeJs+chrome瀏覽器完成<br />
###筆記<br />
&nbsp; &nbsp;1.首先制作html頁面,完成後轉義成jade編碼<br />
&nbsp; &nbsp; &nbsp; 聊天室的頁面基本只有一個頁面,使用的方式是連接時候顯示登陸用戶名界面,<br />
&nbsp; &nbsp; &nbsp; 檢測用戶名沒有問題之後再將登陸界面hide,show出聊天室頁面.<br />
&nbsp; &nbsp;2.完成界面之後,依據界面開發app.js,app.js中需要改造和express結合的socket.io<br />
&nbsp; &nbsp; &nbsp; 具體代碼如下<br />
&nbsp; &nbsp; &nbsp; &nbsp; var server = http.createServer(app);<br />
&nbsp; &nbsp; &nbsp; &nbsp; var io = require('socket.io').listen(server);<br />
&nbsp; &nbsp; &nbsp; 拿到io對像這樣就能對客戶端進行操作了.<br />
&nbsp; &nbsp;3.頁面中作為登陸用戶名的表單需要使用客戶端的socket.io將提交內容通知給服務器端的socket.io<br />
&nbsp; &nbsp; &nbsp; 客戶端的socket對像獲取方法為:<br />
&nbsp; &nbsp; &nbsp; &nbsp; 先導入socket.io.js庫文件,然後 var socket = io.connect();即獲得socket對像<br />
&nbsp; &nbsp; &nbsp; &nbsp; 用戶名需要在客戶端預先驗證是否合法在傳給後台.<br />
&nbsp; &nbsp; &nbsp; &nbsp; 用戶名通過socket.on('username', usernameVal, callback)的方式通知服務器,並且創建一個用戶名是否重名的回調函數<br />
&nbsp; &nbsp;4.服務器端的用戶名使用一個數組保存,檢測用戶名是否重名.<br />
&nbsp; &nbsp; &nbsp; 將用戶名保存在socket中,當連接斷開的時候,將此用戶刪除<br />
&nbsp; &nbsp; &nbsp; 調用客戶端的回調.創建成功就隱藏登陸,顯示聊天室<br />
&nbsp; &nbsp;5.聊天室中的消息默認是保存100條,超過100條會shift掉之前的數據,這個數據是保存在數組中的<br />
&nbsp; &nbsp; &nbsp; *暫未解決的問題: html未轉義,會被腳本侵入（已解決）<br />
&nbsp; &nbsp;6.添加聊天室中登出的操作 添加button,監聽click事件<br />
<br />
###一些改動<br />
&nbsp; &nbsp; 2014-3-11 15:09:07<br />
&nbsp; &nbsp; 1.修改了消息推送的代碼,讓消息推送能夠讓載體div自動滑動到底部以顯示最新的消息<br />
&nbsp; &nbsp; 2.添加用戶連接到聊天室的信息和離開聊天室的信息<br />
&nbsp; &nbsp; 3.添加鍵盤事件 &nbsp;讓sendMessageForm中不用按Post直接Enter也可以發表消息<br />
&nbsp; &nbsp; 4.記錄聊天信息將聊天的所有記錄都儲存在message.txt文本中<br />
&nbsp; &nbsp; 5.修改了登陸後錯誤依然存在的問題 顯示了發言人的顏色<br />
&nbsp; &nbsp; 6.添加title和將發送消息快捷鍵改成Ctrl+Enter<br /><br />
&nbsp; &nbsp; 2014年3月24日10:01:11<br />
&nbsp; &nbsp; 7.添加創建本地存儲文件夾的代碼<br />
<br />
聊天室的東西先做到這裡了 後面想起功能會繼續添加的
