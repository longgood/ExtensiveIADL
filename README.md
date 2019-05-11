# ExtensiveIADL
this the a scriptwise solution for building a extensive IADL
架構
Manager作為資源交換。在下屬的DocManager, CalManager, UIManager

CalManager, 負責將外部感測器與運算的交換整理。
CalManager負責將(感測器)Kinect的資料整理後，傳入TAction中判斷。將所有的動作判斷都放在TActions內作判斷。
答案正確與否的判斷，拉到CalManager來做。

DocManager
讀檔敘述檔，讀外部圖形檔，參數等()

參數讀取:所以會將DocManager當成是一個存取的container, Manager若有需要再從這呼叫，以GetXXX函數方式進行。

UIManager將UI之間的交互整理。
答題剩餘的時間GameObject

# 20190511

* 1.新增結帳，需要注意
a.標籤要怎麼設
b.loading 付款台，預設load wallet嗎?
c.怎麼自動結束?或觸發結束(應該是這個)
d.結束後的話語。回饋。

* 2.其他標籤的干擾
仔細檢查一下。太危險了。
//---actions go
1.讓結帳畫面可以跑。//應該設甚麼樣的標籤。可能涉互動式標籤，讓他的觸發只有在條件滿足時才成立，還是直接NULL過場?
2.結束後的話語與回饋

檢查其他的。


新增NULL。
//--
* 1.新增可以讀兩個resource。
* 2.
# 20190510
快了，快要到了!!
* 按鍵
遲遲無法解決滑鼠按鍵問題
必要時自己重寫，但建議白天清醒時在看過一次程式碼。
或重新一個Scene，看是否有辦法解決問題

我覺得好好研究他的程式碼是個解決方法。
(搞定)
* 結帳
加油

* mTopic
確認其他Topic被影響的程度。
//---
a.一開始就加入清單(OK)
b.結帳按鍵在平常按下會出現北七提醒(只有完成時才會有結帳!!)
c.結帳畫面，自動結束或是找錢。(手動付錢)



///--lesson learned
1.mouse drop is required to add an "InteractionInputModule" script to EventSystem
2.MiddleCanvas->MiddleCamera, is the universal definer of all those 3D object.

# 20190509
* 文字輸出，with color notification(yes,已經大改，目前UI不會更替，會一直存在著，僅改變更換場景的內容值)
* 真3D
* Kinect
//--


畫面上Z軸的位置是可以限制的，但晚一點再來弄吧!

調整Kinect以及draggable 物件的設定條件。
等待，加上計分Counter，計算通過的物品輛，我想就先讓他出現在畫面上吧

動態載入kINECT 以及存取DRAGGABLE 物件okok了，現在
還需要
* 1.多幾組超市物件(OK)
* 2.計分(同時間要升成新的物件，或是移除它的相對parent群組關係。)(帥，完成，並且將Tag移除，確保不會重複計算)
* 3.觸發按鍵(原本已經寫好的，確認是不是因為在不同Canvas,還是???????????????????)
* 4.結帳。
# 20190508
執行順序
* a.時間到直接到結帳(OK)
* b.更新linklist(OK)
* c.計算分數，先用鍵盤模擬(近乎完成)
* d.加入真三D



//--
c.計算分數，將組合出清單文字，其中StoreShopping是否該整個置換，或者只要更新案件文字就好?

每次動作會更新清單上的文字，非常美好的設計，會有預計購買，已經購買的數量。統一用三個顏色

已經達成的用黑色。
未達成的用藍色
而不再品項上的用紅色，

# 20190507
0.產生固定物件(最後才消失)與變換物件(每次切換子場景(wormhole)都會重新生成)。
01.改變切換子場景。{從讀取到的Linklist關聯內取得}
2.讀取Gameobject
3.go!!


執行細節:
a.推車載入(不變的物件 OK)
b.Linklist按鍵(直接生成按鍵好了，不然鍵盤模擬整個方式都不對)，時間到直接結帳。
c.貨櫃的載入(會變動刷新的物件)，換場時刪除變動物件。
d.計算分數(用鍵盤模擬選擇，最後再加入真三D)。
e.真三D(描述檔多一個字串，之後會是   rx:ry:rz,px:py:pz,sx:sy:sz 的格式)我覺得真棒!!!
# 20190504
將水果攤，肉攤，雜物攤，飲料區，衣物區，固定。
題目只提供解答的數量組合。
contentWrong,或另外設定一個，只是來呼叫。

解答的方式，是將多個子場景的解答名稱組合起來。全部正確才算是。


# 20190503
新增子場景控制類別。
在mTopic內加上一個類別"劇本"
會去讀取另外一個所謂的劇本擋，根據劇本黨內的安排，可以執行迴狀關係->單點(結帳)
或是序列關係，或之後定義的關係。

所以在原有的描述檔內，會將每個子場景加上名稱。

這樣將可以完美解決目前的情境布局需求。漂亮。

執行上會影響的包括:
類別的宣稱，讀檔以及排序，NextScene
mTopic:會有"PantoShopping"，對應在描述檔案內，會有多個Shopping SceneName的集合。
NextScene之後若暴力改成3D，再把SceneName當成是定點的標記名稱。

但目前的困境在於，多個不同標記的Scene 互動式物件必須重新載入，或有些需要載入，有些不用，需要詳細區隔開來。Jesus。



Step 1:
定義與執行關係描述檔，PantoScript。會有個陣列List。來描述各場景的連結關係，個別可以一對一或是一對多。一對一若依序往下，就是序列式。一對多，就是複雜關係圖。List的第一個值可以是結帳用。ok

Step 2:

Shopping的場景設定。
每個子場景還需要再加一個敘述檔。
現況是每個櫃子，像是水果/肉品都會有不同的布置。
根據不同的敘述，載入原先已經手動校調好的物件。以及配置方式。所以，contentRight敘述的僅僅是答案的正確性而非選項的載入。或者，這些就寫在contentWrong之中呢?


FINAL:
就手動限定幾個prefab，有個介面能夠觸發一大盤水果，自動(手動)從中選取幾個給予RIGIDBODY COLLIDER等特質。以供選取。
畫面上也提供了隱藏的隔板，讓使用者選取前端的水果，會自動滾下來。

# 20190502
搬遷事宜。
1.檢查RKinectManager是否有更新OK
2.其他的都直接替換OK
3.AVGManager內的LGCloud要拉回來。

待測試，似是已經完成(看一下Display的部分)
以及將互動物件生成時，尺寸是根據原有的比例尺來進行放大縮小。OK(Great)
4.將handmouse的控制改由Kinect來進行。OK
//----
將3D手部抓取的場景加入。
感覺會很酷!


1.一些Kinect互動的Script，等到選擇特定情境時再加入或觸發。
2.資源UI的管理
3.場景更換時，所有UI要重新刷過
4.切換不同場域時，該如何進行。
5.觸發2D的按鈕(原示範場景中有)，來切換到不同的場域。


/--已經完成。
互動觸發的管理，物件的生成，正確性的判斷。
推車內有個判斷物件。
留意這些trigger, tag的設定情況。

/--待處理
1.順序性場景，平行橫向移動的場景。
1.1.按鍵可以選擇移動到不同的地點。
2.切換場景時，尚未選擇的物件移除，但是選擇到的物件不會。
3.清空推車內的物件。

(將物件的相關組件一起複製過去。像是mesh, )
加入主程式。



# 20190430
Come
cal judge內容，cal內建會有的List<string>

# 20190429
a.新增Set標籤，
b.phone call正確完成之前，會等到最後一個號碼輸出在畫面上之後再消失，甚至是能出現個語音。(先完成暫緩消失)
c.每個session都有不同的背景音樂()
d.先用滑鼠模擬0~1之間的活動範圍，在投影放大到該物件的視覺範圍。(mouse is done!!)
讀檔設定正確答案。(完成)
結束時的畫面沒有字(check,ok, 只是因為自行沒有對應到)
按鍵音效，撥通音效(稍後再說)
e. 購物。

規劃
1.NextScene. 要改成可以動態調整場景
2.選擇，會是多選。(1.先從這邊開始)
3.cal.judge, 會算總量(JudgeAfterResponse)
oncompletequize內要跳到結束的場景，這個也要注意。

step
0.回到六個clock情境。多了一個MultiSix,多選，而且劇本檔中若出現重複的依樣不影響。實際的選擇數量可以依照"correct"這個標籤內的數量來訂。所以畫面上會有 
蘋果，蘋果，蘋果，蘋果，番茄，小黃瓜。但只選擇兩個蘋果。那麼在劇本檔中。correct, 會有兩個蘋果，wrong中，會有至少四個選項。但實際選擇只有6-correct.count.
execute:在CalJudge內判斷在這邊判斷，只要名稱跟correct的一樣的就可以了算是正確。


1.測試從單樣多選(蔬果區選兩個蘋果三個鳳梨)，到多樣多選(三旗魚，一醬油)才算正確。
2.新增Set標籤，來進行跳場景。(留意NextScene,CalJudge, OnCompleteQuize)

# 20190426
思考新增ｓｅｔ標籤，讓採購可以使用。　　　
在判斷正確數量選項時，劇本檔中，正確與錯誤的選項會有可能相同，但是總數量已正確地為基準。


考慮加入音樂。
# 20190425
完成正確度驗證，可以正常使用


待改善，不知道為什麼最終的結果出不來。
最後一個數字輸入之後，需要呈現畫面一下子，接著結束告示才出現。

可以在原先２０１７程式中產生對應的設定檔ＰＡＲＡＭ，來給２０１８使用

此刻，緊接著需要確認兩項
一。是否可以用外部檔案控制正確度
二。其他ＴＯＰＩＣ是否仍能正確執行。

# 20190424
先處理電話撥出，
已經將專案移出，可以比較快速的編譯與除錯


在DocManager內紀錄選擇的數字，在CalManager內比對。
JudgeAfterResponse回傳最終的結果。一般是TResponse.Click, then TResponse.Finish
或許可以組成文字，讓畫面呈現。包含錯誤的文字。

---在Judge內重組文字。也判斷。425測試先特定好correctList

# 20190423
新架構一。修改Shopping,
五個或是十個場景為一組Set，
1.組內之間可以互相前往。
2.購買的選項，可以從多個重複項目中選取數個，
3.最終有買齊所需品項。
4.品項會掉到眼前的推車上。
done。

預計會大動到，
1.讀題
2.按鍵選項後
與切換場景選項。
3.出題
反應的接口

看來是個大工程，還有包括手機類別，看來先將專案獨立開來開發。速度才會快。



//----
先忽略RKinectManager，在測試版中直接忽略---->RKinectInteraction。都不能用，只有新增的部分才需要加入。
也忽略LGCloudManager不需要更改。
ParamOrigin--->切記不可以更動到原有的。

# 20190420
將撥電話的物件，直接個體製作一個，但還是適用原先的按鍵物件先組合。

# 20190411
返回鍵 OK
倒數計時
儲存成績，雲端系統。OK
  結果成績顯示 OK->要有成績儲存->ok
*增加UserAction的應用類別。
(可以把資訊都放在List<string>answerCorrect上，只要自行定義好即可。)
  內容可以像是，answerCorrect[0] 名稱,answerCorrect[1] 圖檔。//這是通用的部分
               answerCorrect[2] 互動方式的定義。此後每個定義所需要的資源都是固定的。
               
計算活動度(計算中)OK, 先讀取基本值存在index中，之後再到usermanagement內去計算。
使用者疾病類型。直接新增在usermanagement內  OK

追加，在題目框上頭加上進度文字或是進度條。
追加，單選答對時，在答案選項上的動畫。
追加，使用者的大頭照
# 20190410

AVGParameter
把mTopic移出常態性的儲存，因為只有在GameRoomV3Prefab內，選擇時就已經確認了mTopic
但是有將Difficulty先儲存下來，供之後使用。
參數的儲存與設定，就是該類別的重點。其餘的判定，要拉回到Doc內判定。

加入大project內。花了不少時間在研究加入系統的方法，希望之後改善，或是有個統一的介面窗口。


# 20190409
先以完成出貨產品。包括了加上Kinect,parameter, gameroom，各自的json檔案。
1.Kinect
先放到CalManager的子類別內，先用到HandClock即可。單手雙手。(OK)

2.parameter留意，用不同的parameter與json劇本，來控制。
3.剩下手動控制的選擇。

parameter沒有讀取好，有可能是SaveKiiParameter這個函數被刪除了。可以試試看。
目前統一個一parameter,內有一個Topic隨著不同的訓練，寫入不同的Topic，根據這個Topic，來選定要讀甚麼Json或是在Json裡要怎麼過濾資訊。
# 20190408
待完成項目
0.按電話選擇按電話選擇(OK)
(calmanager內的correctList,以及correctIndex都要修改
--> a.AVGClass把content改成List<string>
  b.讀取Value[CurrentIndex]
  c.修改Repeat Nine CorrectList的內容
  d.參考KinectAsset若手部控制有優化，就用HandMouse
  
  完成，先以四格來計算，之後若是Kinect好操作再來修正。
  
0.活動度計算
1.IADL文字檔讀檔。
2.IADL結束的場景與分數計算。
3.Kinect(包括左右手分別，或是同時的選定)
4.身體活動度選擇




注意事項:
使用的RIOSave...刪除很多函數，加入大專案時，切記不要替代原有檔案。
# 20190405
將該軟體放入主程式內為目標。需要
1.讀取外部檔
2.結束的場景
3.分數的計算
4.加上Kinect
5.測試其他輸入方法。
6.獨立interactive的UI(不要有HandClock出現)OK
7.擦桌子(使用互動式，不一定要全擦完，只要計算有擦多少即可)做完觸發一個 煥然一新的動畫即可，以及動作判定。OK。(或許增加灰塵)讚，完成。
8.若要增加互動式的訓練，完成後的動畫特效。可以在MainManager內的Oncomplete, 延長換場時間。



在Manager的UpdateState內
從Interactive的角度來看。
外頭的是活動反應。_cal, 計算產出0~1的Vector2, UI觸發抹布活動
內頭的是Information, Cal是計算往返幾次，UI是減少髒東西與泡泡。

# 20190404
1.按鍵觸發事件以及進度條(查看之前的結構)
a.把互動，計算(mouse)，UI進度條(UI)，拆開來處理。
b.選擇開始時，送出(滑鼠標得index,以及累計兩秒鐘之後送出觸發到manager)，送出進度條自己計算兩秒。兩秒後的互動，讓avguiinteractive來完成。
  i.Manager(持續的監控取得現在的buttonIndex,不是負一就是按鍵號)，並將資訊送到UIManagery進行圖形，以及決策時間倒數計時(現在UIMouse上這應該要到CalManager)
  ii.UIManager判斷該buttonIndex是新的或是在舊有的上(MouseOver, or Release)，來進行對應的動畫。
  
  當決策時間到數達到兩秒時，會觸發OnClick事件，呼叫Manager上的OnClick,在判定選擇的內容。
  (抓到了，若按鍵Index相同時，應該要有更長的時間冷卻)
  
  iii.選擇時UIManager會觸發對應的動畫，CalManager判定正確性。
  
  
2.能順利完成讀取外部檔案
3.加上Kinect


尚未解決的問題
1.兩隻手繪競相決定誰指定了indexBTN，雖然已經排除了選取過的，但沒有增加另外一隻手指向答案的權利。(會根據angle2index內的判斷順序)
(CalManager, GetHandAngle2Answer要在TAction內，累積同時有兩個符合的答案?)啊，解決了!!!!
2.上一場雨下一場若手一直指向同一個答案，圓環會不見。沒有在對的地方呼叫S(solved)
(解決，先在Manager->NewTraining 開始可以選擇那處，將UIManager內存的Index改成-1。這樣在呼叫decisionBar時，就會出現。)

# 20190403
1.解決了之前的多執行序影響到下個程序問題StopCorountine("DelayAction")，在每個NewTraining開始之前都會先清理。所以就可以用多執行序來排第問題的時間。(似乎還好)
2.讓Question的展開與結束，成為UIManager下的一個類別。(OK)
3.倒數計時器的控制與使用。(OK)
4.單選題若是錯誤就直接TResponse.Crash結束。(ok)
5.將所有的判斷丟到了CalManager, UIManger單純做美術的被指派。(ok)
6.確認了content用來儲存互動答案選項需要的物件名稱與物件檔案名(ok)
a.以四選一或是四多選，會有八個項目。即四個選項個別的title, 與圖檔名
b.或六選一(之後再說)
c.或動作互動前與互動後(觸發的動畫等等)的名稱。
7.順序功能，用answerType來分段。其中correctAnswerList與單選是可以通用的。(ok)
8.handAngle的互動，不要使用滑鼠游標，而是使用指定的，這樣即使答案選項因為解析度的關係重疊了，也不會有錯誤的觸發。
9.背景圖檔若相同，就不重複載入
10.順序選取時，已經正確選過的答案，不應該再被點選到。要在CalManager內將這些選項剃除。

11.連續輸入兩次，要找一下問題出在哪。(時間還是甚麼的?勇敢一點設定進度條有stopmotion, startmotion)

# 20190402
大改整個系統，新增tag, mainmanager, 讓物件搜尋時可以再更快一點。(之後移到主程式中，需要加入)
更改系統方式，handmouse來觸發整體事件，並呼叫mainmanager.內的函數。
1.先控制四選項單選題。讓答對答錯下一題，時鐘物件，整體開始與結束的流程都能順暢。
(尚須時鐘物件，以及自動跳題問題需要解決，可能是控制總答題時間的COROUNTINE沒有完全停止<可以參考前作>)
2.加入CONTENTS，來讓問題選項名稱與品名的影像以及正確答案的設定，都能載入。(4/3)
3.四個選項的順序選題，接著是六個選項(六個選項的pending)
4.其他手動動作/以及JSON檔的輸入
5.雙手/單手的輸入

# 20190326
完成鍵盤的控制handangle,以及觸發相關的按鍵動作。在此以控制mouseIcon的位置，來觸發按鍵。

# 20190312
完成主要的架構。按鍵測試換場OK
可精進處
a.讀取設定的Json文字檔案。
b.事件觸發的音效
c.開頭與結尾的場景
d.增加反應用的GameObject，像是倒水的水滴，等等。(設定好格式之後請孟哲外包)
