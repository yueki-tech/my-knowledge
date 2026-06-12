[一覧に戻る](../index.html)

### SQLPlus

#### ■SQL起動準備
    サーバ接続後、必要の応じて環境変数の設定を行ってからSQLPlusを起動する。
    尚、NLS_LANGは複数言語のサポートの可能。
      $ export NLS_LANGUAGE=Japanese_Japan.AL32UTF8
      $ export NLS_LANGUAGE=Japanese_Japan.AL32UTF8
      $ export ORACLE_HOME=/opt/oracle/product/19.3.0/client_1
      $ export PATH=$PATH:$ORACLE_HOME/bin
      $ sqlplus xxx/xxx@サービス名 @実行ファイル

[一覧に戻る](../index.html)