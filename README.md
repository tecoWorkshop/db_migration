# db_migration

## DB スキーマを管理する方法

1. **DB 管理者にすべての変更を任せる**  
     DB 管理者がボトルネックになった場合に開発が滞る

2. **共有の DB でスキーマを変更する**  
     DB スキーマの変更は基本的にアプリケーションのソースコードにも関わってくるため、  
     スキーマの変更はチーム全体の開発に影響を与えてしまう

3. **DB スキーマのバージョン管理**  
     バージョン管理に必要な要件  
     - どのような環境でも同じ手順で DB の構築が可能なこと
     - 繰り返し再実行が可能なこと
     - テキストファイルであること（マージを簡単にするため）


## DB Migration とは

CDBI (Continuous DataBase Integration: 継続的データベースインテグレーション)

Ruby on Rails のツール名（Migration）から派生

## 機能
- **SQL の適用順とどこまで適用したかを管理する**  
     例）管理テーブルや専用のファイルで、順序やどこまで適用したかを管理する

- **スキーマ定義編集の衝突を管理する**  
     例）SQL ファイルに命名規則を設け、ファイル名が重複したらマージする

- **ロールバックの仕組みを用意する**  
     例）同一ファイルにロールバック用の SQL も記述する（CREATE 文と DROP 文、INSERT 文と DELETE 文）

- **データ（設定データ）のロードもできるようにする**  
     例）SQL ファイルに INSERT 文や UPDATE 文を記述


## DB Migration ツール

- Ruby on Rails  
     http://railsdoc.com/migration

- Fuel PHP  
     http://fuelphp.com/docs/general/migrations.html

- Phpmig  
     https://github.com/davedevelopment/phpmig

- goose (Go)  
     https://bitbucket.org/liamstask/goose



### 使い方（goose）

#### インストール

     $ go get bitbucket.org/liamstask/goose/cmd/goose

#### 設定

     $ mkdir db
     $ cd db
     $ vi dbconf.yml

     development:
          driver: sqlite3
          open: models/app.db

#### マイグレーションスクリプト作成

     $ goose create create_shop sql


#### マイグレーション適用

     $ goose up


#### 状態の確認

     $ goose status



#### ロールバック

     $ goose down



#### バージョン管理用テーブル





