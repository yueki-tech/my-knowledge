[一覧に戻る](../index.html)

### 外部表と内部表

#### ●外部表(駆動表)
    JOINするときのベースになる表。以下のSQLでいえば、table1

    SELECT * FROM table1 t1 INNER JOIN table2 t2 on t1.id = t2.id;

#### ●内部表
    外部表にくっつける表。以下のSQLでいえば、table2

    SELECT * FROM table1 t1 INNER JOIN table2 t2 on t1.id = t2.id;

[一覧に戻る](../index.html)