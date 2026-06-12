[一覧に戻る](../index.html)

### ヒント句

#### ■ヒント句
    ・ヒント句は、Oracleのオプティマイザが作成する実行計画を制御するヒント。
    ・ヒント句を使用することで、結合順、結合方法をオプティマイザに任せず指定することができる。
    ・ヒント句は通常のコメントの構文で、以下のようにコメント(/*+ /)の開始の/*の直後に(+)をつけるのがポイント。
      /*+ ヒント句 */

    具体的には、以下のようにSELECTの後にヒント句を記載する。
    例ではINDEXヒントを指定しており、指定したテーブルに対してインデックススキャンを実行する。

      select /*+ INDEX(employees emp_department_ix)*/ * from ～

    複数のヒントを使用する場合は、以下のようにヒント（例ではLEADINGとUSE_NL）を並べて指定すれば良い。

      select /*+ LEADING (e d) USE_NL(d) */ * from ～ 

    また、ヒント句でのテーブル名は実名でなく別名（エイリアス）を指定する。

    ヒントが使用されない例） 
      select /*+ FULL(DEPARTMENTS) */ * from hr.DEPARTMENTS d where d.manager_id = 200; 

    ヒントが使用される例） 
      select /*+ FULL(d) */ * from hr.DEPARTMENTS d where d.manager_id = 200; 

    別名を使用していない場合は、以下のようにテーブル名をそのまま指定できる。

      select /*+ FULL(DEPARTMENTS) */ * from hr.DEPARTMENTS where manager_id = 200;

    通常はOracleのオプティマイザが統計情報を参照して最適な実行計画を選択してくれるものの、
    オプティマイザ統計が古くて実態とかけ離れていたり、複雑なSQLの場合は（7つ以上の表を結合するなど）、
    最適な実行計画とならないことがありえる。そのようなときに実行計画に対するヒントを使用する。
    
    このように便利なヒント句だが、実際のデータが変わることにより、
    使用したヒントで作成された実行計画が最適ではなくなることもありえる。
    ヒント句がなければオプティマイザが最適な実行計画を選択するが、
    ヒント句があるために最適な実行計画が選ばれなくなってしまうことがある。
    
    ヒント句はたくさんあるものの、実際によく使うヒントはLEADING, USE_NL, INDEX, FULL, USE_HASH。

      LEADING  
      USE_NL  
      INDEX  
      FULL  
      USE_HASH  

#### ●LEADING
    LEADINGヒントは、表を結合する順序を指定できる。
    大抵はUSE_NL/USE_HASHヒントと組み合わせて利用する。

    構文： LEADING([表名] [表名] ・・・)

    例： /*+ LEADING(a b c)

#### ●USE_NL
    USE_NLヒントは、指定された各表をネステッドループ結合(nested loop join)で結合する。
　
#### ●NESTED LOOP
    nested loopはオプティマイザがアクセス対象のデータが比較的少ない場合に選択されることが多い結合方法。

    以下は実行例。
    ※最適化としては意味がないが実行計画の行数が少なくなるようにFULLヒントを使用。

    構文： USE_NL([内部表1] [内部表2] ・・・)

    例： /*+ LEADING(A B C) USE_NL(B C) */

      select /*+ FULL(b) FULL(a) LEADING(a b) USE_NL(b) */ * from departments a, employees b where a.manager_id = b.manager_id;

#### ●USE_HASH
    USE_HASHヒントは、指定された各表をハッシュ結合を使用して結合する。
    通常LEADINGヒントと一緒に使用する。

    構文： USE_HASH([内部表1] [内部表2] ・・・)

    例： /*+ LEADING(A B C) USE_HASH(B C) */

    3つの表でハッシュ結合した場合の例。
    LEADINGヒントでa,b,cと指定しているので、最初にaとbで結合し、その後にその結果とcを結合している。

      select /*+ FULL(c) FULL(b) FULL(a) LEADING(a b c) USE_HASH(b c) */ * from departments a, employees b, locations c where a.manager_id = b.manager_id and a.location_id = c.location_id; 

    また、ハッシュ表を指定する場合は、SWAP_JOIN_INPUTSヒントを使用する。
    SWAP_JOIN_INPUTS(表別名)で、指定した表がハッシュ表として利用されるようになる。

#### ●FULL
    FULLヒントは、指定した表に対してフルスキャンを実行する。

    構文： FULL([表名])

    例： /*+ FULL(A) */

    以下はFULLヒントを使用した実行例。

      select /*+ FULL(b) */ * from employees b where b.last_name = 'King';

#### ●INDEX
    INDEXヒントは、指定した表に対してインデックススキャンを実行します。

    構文： INDEX([表名] [インデックス名])

    例： /*+ INDEX(A IDX) */
    ※表の別名AのIDXインデックスを使用する場合

    以下はINDEXヒントを使用した実行例。

      select /*+ INDEX(b EMP_NAME_IX) */ * from employees b where b.last_name = 'King';

[一覧に戻る](../index.html)