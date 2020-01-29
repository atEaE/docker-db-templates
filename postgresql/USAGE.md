# 接続方法まとめ
## Windows
### A5:mk-2
1. A5:mk-2を起動する。  
   データベースの追加からPostgreSQLを選択する。
   ![Add DB](./docs/windows/01_add-db.png)

2. 接続設定の画面が表示されるので、Dockerの設定情報に合わせて設定を行う。
   ![Settings](./docs/windows/02_setting.png)

3. テスト接続を行い、設定情報に誤りがないことを確認する。  
   設定情報が正しければ、下記のポップアップが出現する。
   ![Test Connect](./docs/windows/03_test-connect.png)

4. 最後に実際にDBへ接続を行う。  
   先ほどと同様に設定情報を入れて、接続を行う。
   ![Connect](./docs/windows/04_connect.png)  
   
   接続に成功すると、サイドメニューのTreeViewに構造が表示される。
   ![Check](./docs/windows/05_check.png)
