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
# 20190410

AVGParameter
把mTopic移出常態性的儲存，因為只有在GameRoomV3Prefab內，選擇時就已經確認了mTopic
但是有將Difficulty先儲存下來，供之後使用。
參數的儲存與設定，就是該類別的重點。其餘的判定，要拉回到Doc內判定。


# 20190409
先以完成出貨產品。包括了加上Kinect,parameter, gameroom，各自的json檔案。
1.Kinect
先放到CalManager的子類別內，先用到HandClock即可。單手雙手。(OK)

2.parameter留意，用不同的parameter與json劇本，來控制。


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
