[一覧に戻る](../index.html)

### Maven

#### ■Mavenの設定
    ・C:¥mavenなどに配置。
    ・システム環境変数「M2_HOME」追加
      変数名：M2_HOME
      変数値：C:\maven
    ・システム環境変数「Path」のリストに「%M2_HOME%\bin」を追加
    ・C:¥maven\conf\settings.xmlに以下を設定。
      proxy　⇒アカウント、パスワード、ホスト、ポート、ノンプロキシーホストを設定する。
      server　⇒ID、ユーザー名、パスワードを設定 ※proxyのアカウントやパスワードとは異なる点に注意。
    ・eclipseの設定にMavenを追加
      ①「Maven」－「インストール」の「追加」ボタンを押下
      ②「C:\Maven」を選択し、リストに追加されたMavenをチェックして適用する。
      ③「Maven」－「ユーザー設定」のユーザー設定の「参照」ボタンを押下
      ④「C:\Maven\conf\settings.xml」を選択して適用する。

#### ■Java Mavenプロジェクト
    ・C:¥Users\[username]\.m2\repository配下にpomの依存関係がビルド時に自動的にダウンロードされる。
      通常は.m2及びrepositoryフォルダは自動的に作成される。

    ①TortoiseSVNなどでgitからクローンしてきたソースから、pom.xmlのあるフォルダが
    プロジェクトの対象であり、そのフォルダで以下のコマンドを実行。
      mvn eclipse:eclipse　・・・実行後、「BUILD SUCCESS」が出たらOK
      mvn clean package　・・・ビルドが実行される。
      mvn clean package -Plocal・・・ローカルビルドの場合
      ※ビルドエラーになる場合は、mvn eclipse:eclipseから再実施してみる
    ②eclipseの「ファイル」メニューから「ファイル・システムからプロジェクトを開く」を選択し、
    上記①のフォルダを選択して開く。
    ③ソース修正後は再度「mvn clean package -Plocal」を実行してclassファイルを更新する
    (eclipseのクリーンビルドでは更新されない)

    【トラブル対応】
      ・上記②でリポジトリ－の更新がうまくいかない場合、eclipseからプロジェクトを削除
      (ソースまでは削除しない)、.m2\repositoryを削除(orリネーム)して、mvn eclipse:eclipseで
      作成されたプロジェクトフォルダの.projectファイルやtargetフォルダなどを削除、
      再度mvn clean cleanから再実施する。
      その際、PCの再起動やeclipseでプロジェクトを開く際に「ネストされたプロジェクトの検索」
      のチェックも付ける。
      mavenのコマンドプロンプトは管理者で実行してみる。
      ・上記③でビルド時にライブラリが削除できないエラーが出た場合、eclipseをいったん終了させるとうまくいく。

      プロジェクトの依存関係を確認したい場合は以下の通り。
        ①eclipseのプロジェクトを右クリックし、「コマンド・プロンプト」を開く
        ②「mvn dependency:tree -f pom.xml」を実行

[一覧に戻る](../index.html)