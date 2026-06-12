[一覧に戻る](../index.html)
    
### 権限関連 
    
    ■現行ユーザーが権限受領者であるオブジェクトの権限付与を示す方法
    （自身に付与されている権限）
      ※WHERE句は任意
      
      SELECT * FROM USER_TAB_PRIVS_RECD
      WHERE TABLE_NAME IN ('テーブル名','テーブル名')
    
    ■現行ユーザーがオブジェクト所有者、権限付与者または権限受領者であるオブジェクトの権限付与を示す方法
      ※WHERE句は任意
    
      SELECT * FROM USER_TAB_PRIVS
      WHERE TABLE_NAME IN ('テーブル名','テーブル名')

[一覧に戻る](../index.html)