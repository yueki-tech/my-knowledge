[一覧に戻る](../index.html)

### 実行計画
    
#### ■実行計画
    
    ・実行計画を確認する方法はいくつもあるが、ここではSQLPlusで接続し、DBMS_XPLANを使用する。
      SQLPlusでDBへ接続し、以下のようにコマンドを実行して確認する。
      
      set serveroutput off 
      set linesize 1000 
      set pagesize 0
      
      ※実行計画を表示するSQLを実行する。 
      select /*+ FULL(d) */ * from hr.DEPARTMENTS d where d.manager_id = 200; 
    　
    ・SQL実行後、DBMS_XPLAN.DISPLAY_CURSORを使用して直前に実行したSQLの実行計画を表示する。
    　
      select * from table(DBMS_XPLAN.DISPLAY_CURSOR format=>'ALL LAST')); 
      
      ※一部省略。formatは色々とオプションがある。最低限で良ければBASICを指定します。
      ※ヒント句を扱うには実行計画が読める必要がある。
    　
    ・直前に実行したSQLの実行計画を取得する方法
      
      SQL> set serveroutput off 
      →　正しく取得できないので、「set serveroutput off」は必ず実行。
      
      SQL> set linesize 1000 
      SQL> set pagesize 0 
      →　折り返しやページ変更が発生しないように設定。 
      
      SQL> select emp.first_name, emp.last_name, j.job_title from employees emp, jobs j where emp.job_id = j.job_id and emp.salary = 8300.00; 
      →　実行計画を取得するSQLを実行。
      
      SQL> select * from table(DBMS_XPLAN.DISPLAY_CURSOR()); 
      →　実行計画取得。DBMS_XPLAN.DISPLAYを引数なしで呼ぶ。引数なしだと直前に実行したSQLの実行計画を取得できる。 
    
    ・実行計画の取得対象から除外するにはSQLファイルの中で以下のように記述。
      exec DBMS_STATS.LOCK_TABLE_STATS('スキーマ名','テーブル名')
    
[一覧に戻る](../index.html)