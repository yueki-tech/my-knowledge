# パフォーマンス・性能測定

[一覧に戻る](../index.html)

## パフォーマンス・性能測定

### ■性能測定
    ・DBSTAT
    　・コンソールで1秒おきにstatを出力する場合
    　　⇒　vmstat -tn 1
    
    　・ファイルで1秒おきにstatを出力する場合
    　　⇒　vmstat -n 1 | awk '{"date \x27+%Y/%m/%d %H:%M:%S\x27" | getline d; print d " " $0; close("date \x27+%Y/%m/%d %H:%M:%S\x27")}' | tee ./vmstat_outoput_test.txt
    
    ・PIDSTAT
    　・プロセス番号を確認してから、その番号を指定してpidstatを確認する
    　　⇒　ps -ef | grep /usr/java/current/bin/java
    　　⇒　pidstat -p 99999 -u 1

    <a href="../index.html">一覧に戻る</a>
