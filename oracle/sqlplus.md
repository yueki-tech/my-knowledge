[一覧に戻る](../index.html)

### SQLPlus

#### ■SQL起動準備
    サーバ接続後、必要に応じて環境変数の設定を行ってからSQLPlusを起動する。
    尚、NLS_LANGは複数言語のサポート可能。
      $ export NLS_LANGUAGE=Japanese_Japan.AL32UTF8
      $ export NLS_LANGUAGE=Japanese_Japan.AL32UTF8
      $ export ORACLE_HOME=/opt/oracle/product/19.3.0/client_1
      $ export PATH=$PATH:$ORACLE_HOME/bin
      $ sqlplus xxx/xxx@サービス名 @実行ファイル

#### コンソール出力調整
    SQL> SET LIN 300
    SQL> SET PAGES 1000
    SQL> SET WRAP OFF
    SQL> SET COLSEP ','   ※Tabをカンマに変換して表示したい場合のみ

#### 表示件数制限
    Oracle ⇒ fetch first 10 rows only
    PostgresSQL ⇒ limit 10

[一覧に戻る](../index.html)