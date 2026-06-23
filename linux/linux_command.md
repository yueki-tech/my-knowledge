[一覧に戻る](../index.html)

### Linuxコマンド

#### ■所有者変更
    chown user:group ./test.txt

#### ■権限変更
    chmod 644 ./test.txt

#### ■グレップ（grep）
    grepした結果をファイルに出力する
      grep hoge /etc/passwd > /home/someone/list.txt

#### ■ファイル転送（scp）
    転送元にファイルを配置の上、転送元に接続し、以下のコマンドを実行する。
    scp (転送元ファイルのパス) (転送先ホスト名):(転送先ディレクトリ)

#### ■テキストの置換、削除、抽出、追加などの加工（sed）
    sedコマンドでファイルのtab文字をカンマに変更する
      sed -i 's/\t/,/g' ./sample.txt

    sedコマンドでファイル最終行の改行を削除する
      set -i '${/^$/d}' ./sample.txt

#### ■プロセスの確認
    ・全プロセス
      ps -ef

    ・httpdプロセスを検索し、自身のgrepプロセスは除外する方法
      ps -ef | grep httpd | grep -v 'grep httpd'

    ・tomcatプロセスを検索し、自身のgrepプロセスは除外する方法
      ps -ef | grep java | grep -v 'grep java'

#### ■バックグランド実行方法
    バックラウンドで実行することにより、コンソールのセッションが切れても実行が途切れない。
      nohup sh /aaa/aaa.sh &

#### ■vmstatの出力方法
    現在のディレクトリにtest.txtという名前でファイルに出力する場合。（終了はCtrl+C）
      vmstat -n 1 | awk '{"date \x27+%Y/%m/%d %H:%M:%S\x27" | getline d; print d " " $0; close("date \x27+%Y/%m/%d %H:%M:%S\x27")}' | tee ./test.txt

#### ■プロセスの強制終了
    ①「ps -l | grep find」などで終了したいプロセスのPIDを確認する。
    ②PIDが100なら「kill 100」でプロセスを終了する。
      ※「ps -l」は自分のプロセスを表示する。

[一覧に戻る](../index.html)