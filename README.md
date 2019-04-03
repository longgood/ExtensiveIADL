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
7.順序功能，用answerType來分段。其中correctAnswerList與單選是可以通用的。
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
