[一覧に戻る](../index.html)

### シェル関連

#### ■変数のセットと使い方
    dir=/home/someone/
    filepath="$dir"sample.txt

#### ■シェル実行前の環境変数の読み込み例(test.conf)
    export DBSERVER HOST=
    export ORACLE_BASE=
    export ORACLE_HOME=
    export ORACLE_SID=
    export PATH=$PATH:$ORACLE_HOME/bin
    export ORACLE_USR=
    export ORACLE_PWD=
    export LOG_FILE_DIR=
    export LOGFILE="${LOG_FILE_DIR}/test_$(date +%Y%m%d%H%M%S).log"

#### ■シェルの実装例(test.sh)
    #!/bin/sh
    source ./test_conf.txt
    
    #ログファイルに標準出力及びエラー出力を行う
    exec >> "${LOG_FILE}" 2>&1
    
    #SQL実行結果を変数AAAに書き込む(「<< EOF」が以降の出力を読み込む命令となっている)
    AAA=`sqlplus -s ${ORACLE_USR}/${ORACLE_PWD}@${TNSNAME} << EOF
    set heading off;
    select test_name from test_table where id='1';
    exit;
    EOF`

[一覧に戻る](../index.html)