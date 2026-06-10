[一覧に戻る](../index.html)

### MyBatis

#### ■基礎知識
    ・基礎知識 参考サイト①
      qiita.com/TaikiTkwkbysh/items/9f598ed01c363b59fd98

    ・基礎知識 参考サイト②(カラムマッピング)
      MyBatisにはカラム名とソースコードのフィールド名とのマッピングの仕組みがある。
      qiita.com/yu_bookstore/items/f2563c2105cadeced6d0

    ・BeanからInterfaceのMapperを介してxmlで定義したSQLを実行。
      Mapperの戻り値をEntityクラスのList型(List&lt;xxEntity&gt;)にして返却
      　
    ・xmlファイル内のifタグでSQL文を動的に変えている
      <if test="...Flg">
        ,columna
      </if&>

#### ■プロパティーマスタから値を取得する実装例
    ①プロパティーマスタ
      KEY：key
      VALUE：value

    ②Property.xmlファイル
      <select id="getProperty"
        resultType="jp.co.test.model.entity.PropertyEntity"
        parameterType="String">
        select
        <include refid="propertyColumns" />
        from m_property p
        where
        p.key = #{key} and
        p.delete_flg = '0'
      </select>

    ③PropertyMapper.java
      Public interface PropertyMapper {
        PropertyEntity getProperty(String key);
      }

    ④TestUtil.java
      public static String getProperty(String key) throws PropertyNotFoundException {
        SqlSession session = getSqlSession();  // システム毎にセッション取得の実装は異なるため詳細は割愛
        PropertyMapper mapper = session.getMapper(PropertyMapper.class);
        PropertyEntity entity = mapper.getProperty(key);
        return (entity==null) ? null : entity.getValue();
      }

    ⑤Test.java
      …
        String ret = TestUtil.getProperty("key");
      …

[一覧に戻る](../index.html)