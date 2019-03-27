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

# 20190326
完成鍵盤的控制handangle,以及觸發相關的按鍵動作。在此以控制mouseIcon的位置，來觸發按鍵。

# 20190312
完成主要的架構。按鍵測試換場OK
可精進處
a.讀取設定的Json文字檔案。
b.事件觸發的音效
c.開頭與結尾的場景
d.增加反應用的GameObject，像是倒水的水滴，等等。(設定好格式之後請孟哲外包)
