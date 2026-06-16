[一覧に戻る](../index.html)

### A5SQL
    
#### ■コンソールに出力する方法
    A5SQLのコンソールにDBMS_OUPUT.PUT_LINEのメッセージを表示するには、以下のようにDBMS_PUTLINE.ENABLEメソッドで有効化して出力を行う。
    
      DBMS_OUTPUT.ENABLE;
      -- SQL文出力
      DBMS_OUTPUT.PUT_LINE('TEST MESSAGE');

[一覧に戻る](../index.html)