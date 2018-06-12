# マイグレーション(migration)
## マイグレーションとは
### マイグレーションとは
直接SQLを使わずに、データベースのテーブルやカラムなどの構造を変更できる仕組み

### 特徴
- db/migrateディレクトリ以下にあるRubyで書かれたファイル
- ファイル名はタイムスタンプ(西暦、月、日、時、分、秒)とアンダースコア(_)で始まり、クラス名のすべての大文字を小文字にしたもの
- 別々のマイグレーションファイルに同じ名前のマイグレーションクラスを記述できない
- idという主キーを自動的に追加
- 実行するにはRakeタスク
- schema_infoテーブルに現在のバージョンが格納

### 簡単な例
```ruby
class AddSsl < ActiveRecord::Migration
  def up
    add_column :accounts, :ssl_enabled, :boolean, default: true
  end

  def down
    remove_column :accounts, :ssl_enabled
  end
end
```
```ruby
class TenderloveMigration < ActiveRecord::Migration
  def change
    create_table(:horses) do |t|
      t.column :content, :text
      t.column :remind_at, :datetime
    end
  end
end
```

### 利用可能なメソッド
- create_table
- drop_table
- change_table
- rename_table
- add_column
- rename_column
- change_column
- remove_column
- add_index
- remove_index
- remove_index

### サポートしているデータベース
- MySQL
- PostgreSQL
- SQLite
- SQL Server
- Sybase
- Oracle

## テーブルの作成(create_table)
### 説明
テーブルを作成

### 使い方
```ruby
create_table(テーブル名 [, オプション])
```
```ruby
create_table テーブル名  [, オプション] do |t|
  t.型 カラム名  [, カラムオプション]
end
```

### オプション

| オプション   | 説明                                     | デフォルト |
| :----------- | :--------------------------------------- | :--------- |
| :id          | 主キーを自動生成                         | true       |
| :primary_key | 主キーのカラムの名前                     | id         |
| :options     | テーブルオプション                       |
| :temporary   | 一時テーブルとして作成                   | false      |
| :force       | テーブルを作成前に、既存のテーブルを削除 | false      |
| :as          |

### カラムオプション

| オプション | 説明             | デフォルト |
| :--------- | :--------------- | :--------- |
| :limit     | カラムの桁数     |
| :default   | デフォルトの値   |
| :null      | nullを許可するか | true       |
| :precision | 数値の桁数       |
| :scale     | 小数点以下の桁数 |

### カラムの型

| データ方  | 説明           |
| :-------- | :------------- |
| string    | 文字列         |
| text      | 長い文字列     |
| integer   | 整数           |
| float     | 浮動小数       |
| decimal   | 精度の高い小数 |
| datetime  | 日時           |
| timestamp | より細かい日時 |
| time      | 時間           |
| date      | 日付           |
| binary    | バイナリデータ |
| boolean   | Boolean型      |

### 例
テーブルの作成
```ruby
crate_table :products do |t|
  t.string :name
end
```

空のカラムを禁止
```ruby
create_tabe :products |t|
  t.string :name, :null => false
end
```

文字コードを指定してテーブルを作成
```ruby
create_table :suppliers, :options => 'ENGINE=InnoDB DEFAULT CHARSET=utf8'
```

主キーを指定してテーブルを作成
```ruby
create_table(:objects, :primary_key => 'guid') do |t|
  t.column :name, :string, :limit => 80
end
```

プライマリーキーの無いテーブルを作成
```ruby
create_table(:categories_suppliers, :id => false) do |t|
  t.column :category_id, :integer
  t.column :supplier_id, :integer
end
```

## テーブル名を変更(rename_table)
### 説明
指定したテーブルの名前を変更する

### 使い方
```ruby
rename_table(現在のテーブル名, 新しいテーブル名)
```

### 例
now_tableからnew_tableに変更
```ruby
rename_table :now_table, :new_table
```

## テーブルの削除(drop_table)
### 説明
指定したテーブルを削除

### 使い方
```ruby
drop_table(:テーブル名 [, オプション])
```

### オプション

| オプション   | 説明                                     | デフォルト |
| :----------- | :--------------------------------------- | :--------- |
| :id          | 主キーを自動生成                         | true       |
| :primary_key | 主キーのカラムの名前                     | id         |
| :options     | テーブルオプション                       |
| :temporary   | 一時テーブルとして作成                   | false      |
| :force       | テーブルを作成前に、既存のテーブルを削除 | false      |

### 例
productsテーブルを削除
```ruby
drop_table :products
```

## カラムの追加(add_column)
### 説明
指定したテーブルにカラムを追加

### 使い方
```ruby
add_column(テーブル名 カラム名, タイプ [, オプション])
```
```ruby
change_table テーブル名 do |t|
  t.タイプ カラム名 [, オプション]
end
```

### オプション

| オプション | 説明                          | デフォルト |
| :--------- | :---------------------------- | :--------- |
| :limit     | カラムの桁数を指定            |
| :default   | デフォルト値を指定            |
| :null      | nill値を許可するか            | true       |
| :precision | :decimal 型の精度を指定       |
| :scale     | :decimal 型の小数点以下の桁数 |

precisionとscaleについては、データベースによって差があるので注意が必要

### 例
postsテーブルにtitleカラムを作成
```ruby
def self.up
  add_column :posts, :title, :string
end
```

カラムの桁数が10桁
```ruby
def self.up
  add_column :posts, :title, :string, :limit => 10
end
```

null値を許可しない
```ruby
def self.up
  add_column :posts, :title, :string, :null => false
end
```

## カラム名の変更(rename_column)
### 説明
指定したテーブルのカラム名を変更

名前を変更しても、そのカラムに関連付けられている既存のデータは破棄されない

### 使い方
```ruby
rename_column(テーブル名, 変更するカラム名, 新しいカラム名)
```
```ruby
change_table テーブル名 do |t|
  t.rename 変更するカラム名, 新しいカラム名
end
```

### 例
usersテーブルのe_mailカラムをmailに変更
```ruby
class RenameEmailColumn < ActiveRecord::Migration
  def self.up
    rename_column :users, :e_mail, :mail
  end
  def self.down
    rename_column :users, :mail, :e_mail
  end
end
```

## カラムの変更(change_column)
### 説明
既存のカラムの定義を変更

### 使い方
カラムの変更
```ruby
change_column(テーブル名,  カラム名, データ型 [, オプション])
```

カラムのデフォルト値の変更
```ruby
change_column_default(テーブル名,  カラム名, デフォルト値)
```

### オプション

| オプション | 説明                          |
| :--------- | :---------------------------- |
| :limit     | カラムの桁数を指定            |
| :default   | デフォルト値を指定            |
| :null      | nill値を許可するか            |
| :precision | :decimal 型の精度を指定       |
| :scale     | :decimal 型の小数点以下の桁数 |

### 例
usersテーブルのnameカラムをtext型に変更
```ruby
change_column(:users, :name, :text)
```

文字数の最大を80に変更
```ruby
change_column(:users, :name, :string, :limit => 80)
```

null側を許可しないように変更
```ruby
change_column(:users, :name, :string, :null => dalse)
```

### カラムの削除(remove_column)
## 説明
指定したテーブルのカラムを削除

### 使い方
```ruby
remove_column(テーブル名, カラム名 [, 型, オプション])
```

### オプション

| オプション | 説明                          | デフォルト |
| :--------- | :---------------------------- | :--------- |
| :limit     | カラムの桁数を指定            |
| :default   | デフォルト値を指定            |
| :null      | nill値を許可するか            | true       |
| :precision | :decimal 型の精度を指定       |
| :scale     | :decimal 型の小数点以下の桁数 |

### 例
usersテーブルのdescriptionカラムを削除
```ruby
remove_column(:users, :description)
```

## インデックスの追加(add_index)
### 説明
指定したテーブルにインデックスを追加

### 使い方
```ruby
add_index(テーブル名, インデックスを付与するカラム名 [, オプション])
```
```ruby
change_tabe テーブル名 do |t|
  t.index ンデックスを付与するフィールド名 [, オプション]
end
```

### オプション

| オプション | 説明                                   |
| :--------- | :------------------------------------- |
| :name      | インデックスの名前                     |
| :unique    | trueを指定するとユニークなインデックス |
| :length    | インデックスに含まれるカラムの長さ     |

### 例
usersテーブルのnameカラムのインデックスを生成
```ruby
add_index :users, :name
```

ユニークなインデックスを生成
```ruby
add_index :users, [:name, :employee_id], :unique => true
```

インデックス名をつけて生成
```ruby
add_index :users, [:name, :employee_id], :unique => true, :name => 'by_branch_name'
```

インデックスの長さを10に指定して生成
```ruby
add_index :users, :name, :name => 'by_name', :length => 10
```

## インデックスの削除(remove_index)
### 説明
指定したテーブルのインデックスを削除

### 使い方
```ruby
remove_index(テーブル名 [, オプション])
```
```ruby
change_table テーブル名 do |t|
  t.remove_index インデックス名
end
```

### オプション

| オプション                                | 説明           |
| :---------------------------------------- | :------------- |
| :name => インデックス名                   | インデックス名 |
| :column => インデックスを構成するカラム名 | カラム名       |

### 例
usersテーブルのnameカラムのインディックスを削除
```ruby
remove_index :users, :name
```

## created_atとupdated_atを生成(timestamps)
### 説明
created_atとupdated_atを両方追加するメソッド

### 使い方
```ruby
timestamps
```

### 例
usersテーブルにtimestampsを設定
```ruby
create_table :users do |t|
  t.timestamps
end
```

## リファレンスの生成(references)
### 説明
他のテーブルへの外部キーを表すカラムを生成

### 使い方
```ruby
references
```

### 例
belongs_to :user_idと同じ
```ruby
create_table :blogs do |t|
  t.references("user")
end
```

## データベースのカラムをバージョンアップ(up)
### 説明
データベースのカラムをバージョンアップする。

Rails3.0以下のバージョンのself.upに相当するのは、changeメソッド。

Rails3.1以上で、upメソッドはロールバックできない処理をする際に主に使用する。

### 使い方
```ruby
def up
end
```

### 例
pagesテーブルにnameカラムをstring型で作成
```ruby
def up
  create_table :pages do |t|
    t.string :name
    t.string :category
  end
end
```

## データベースのカラムをバージョンダウン(down)
### 説明
データベースのカラムをバージョンダウンする。

Rails3.0以下では、self.upとself.downをセットに記述していたが、Rails3.1ではchangeメソッドのみで両方の処理を実行する。

Rails3.1以上では、downメソッドはロールバックできない処理の際に主に使用する。

### 使い方
```ruby
def down
end
```

### 例
基本的な使い方
```ruby
def down
  drop_table :pages
end
```

## データベースのカラムを変更(change)
### 説明
データベースのカラムを変更する

### 使い方
change(カラム名, 型 [, オプション])

### 例
```ruby
t.change(:name, :string, limit: 80)
```
```ruby
t.change(:description, :text)
```

## マイグレーションファイルでSQLを実行(execute)
### 説明
マイグレーションファイルでSQLを実行する

### 使い方
```ruby
execute SQL文
```

### 例
pagesテーブルの最新の10件を取得
```sql
execute "SELECT * FROM pages ORDER BY updated_at DESC LIMIT 10"
```

## カラムが存在するかチェック(column_exists?)
### 説明
指定したテーブルにカラムが存在するかチェックする

### 使い方
```ruby
column_exists?(テーブル名, カラム名 [, 型, オプション])
```

### オプション

| オプション   | 説明                                     | デフォルト |
| :----------- | :--------------------------------------- | :--------- |
| :id          | 主キーを自動生成                         | true       |
| :primary_key | 主キーのカラムの名前                     | id         |
| :options     | テーブルオプション                       |
| :temporary   | 一時テーブルとして作成                   | false      |
| :force       | テーブルを作成前に、既存のテーブルを削除 | false      |

### 例
pagesテーブルのtitleカラムにインデックスが存在するか
```ruby
column_exists? :pages, :title
```

## インデックスが存在するかチェック(index_exists?)
### 説明
指定したテーブルにインデックスが存在するかチェックする

### 使い方
```ruby
index_exists?(テーブル名, カラム名 [, オプション])
```

### オプション

| オプション | 説明                                   |
| :--------- | :------------------------------------- |
| :name      | インデックスの名前                     |
| :unique    | trueを指定するとユニークなインデックス |
| :length    | インデックスに含まれるカラムの長さ     |

### 例
pagesテーブルのtitleカラムにインデックスが存在するか
```ruby
index_exists? :pages, :title
```

## テーブル定義を変更(change_table)
### 説明
テーブル定義を変更する

### 使い方
```ruby
change_table(テーブル名 [, オプション]) do |t|
  t.メソッド名(データ型) カラム名
end
```

### オプション

| オプション | 説明                                   | デフォルト |
| :--------- | :------------------------------------- | :--------- |
| :bulk      | 変更内容を1つのALTER TABLEにまとめるか | false      |

### 使用できるメソッド

| メソッド名        | 説明                       |
| :---------------- | :------------------------- |
| index             | インデックス               |
| change            | カラムを変更               |
| change_default    | カラムのデフォルト値を変更 |
| rename            | カラムの名前を変更         |
| remove            | カラムを削除               |
| remove_references | リファレンスの削除         |
| remove_index      | インデックスの削除         |
| remove_timestamps | タイムスタンプの削除       |

### データ型

| メソッド名 | 説明           |
| :--------- | :------------- |
| string     | 文字列         |
| text       | 長い文字列     |
| integer    | 整数           |
| float      | 浮動小数       |
| decimal    | 精度の高い小数 |
| datetime   | 日時           |
| timestamp  | より細かい日時 |
| time       | 時間           |
| date       | 日付           |
| binary     | バイナリデータ |
| boolean    | Boolean型      |

### 例
pagesテーブルにtext型のmemoを追加、titleにインデックスを設定
```ruby
change_table :pages do |t|
  t.text :memo
  t.index :title
end
```

カラムの追加
```ruby
change_table(:suppliers) do |t|
  t.column :name, :string, limit: 60
end
```

2つのカラムの追加
```ruby
change_table(:suppliers) do |t|
  t.integer :width, :height, null: false, default: 0
end
```

## リファレンスの追加(add_reference)
### 説明
既存のテーブルにリファレンスを追加する

### 使い方
```ruby
add_reference(テーブル名, リファレンス名 [, オプション])
```

### オプション

| オプション   | 説明                   |
| :----------- | :--------------------- |
| :polymorphic | ポリモーフィックを付与 |
| :index       | インデックスを付与     |

### 例
オプションなし
```ruby
add_reference(:products, :user)
```

オプションあり
```ruby
add_reference(:products, :supplier, polymorphic: true, index: true)
```

## created_atとupdated_atを追加(add_timestamps)
### 説明
既存のテーブルにcreated_atとupdated_atを追加する

### 使い方
```ruby
add_timestamps(テーブル名)
```

### 例
usersテーブルにcreated_atとupdated_atを追加
```ruby
add_timestamps(:users)
```

## カラムの初期値を設定(change_column_default)
### 説明
カラムの初期値を設定する

### 使い方
```ruby
change_column_default(テーブル名, カラム名, 初期値)
```

### 例
```ruby
change_column_default(:suppliers, :qualification, 'new')
```
```ruby
change_column_default(:accounts, :authorized, 1)
```
```ruby
change_column_default(:users, :email, nil)
```

## テーブルを結合して作成(create_join_table)
### 説明
2つのテーブルを結合して新しいテーブルを作成する

### 使い方
```ruby
create_join_table(テーブル1, テーブル2 [, オプション]) do |td|
end
```

| オプション      | 説明                                     |
| :-------------- | :--------------------------------------- |
| :table_name     | テーブルの名前                           |
| :column_options | カラムのオプション                       |
| :options        | オプション                               |
| :temporary      | 一時テーブルとして作成                   |
| :force          | テーブルを作成前に、既存のテーブルを削除 |

### 例
```ruby
create_join_table(:assemblies, :parts, options: 'ENGINE=InnoDB DEFAULT CHARSET=utf8')
# CREATE TABLE assemblies_parts (
#   assembly_id int NOT NULL,
#   part_id int NOT NULL,
# ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

## join_tableを削除(drop_join_table)
### 説明
join_tableを削除する

### 使い方
```ruby
drop_join_table(テーブル1, テーブル2 [, オプション])
```

### オプション

| オプション      | 説明                                     |
| :-------------- | :--------------------------------------- |
| :table_name     | テーブルの名前                           |
| :column_options | カラムのオプション                       |
| :options        | オプション                               |
| :temporary      | 一時テーブルとして作成                   |
| :force          | テーブルを作成前に、既存のテーブルを削除 |

### 例
```ruby
drop_join_table(:assemblies, :parts, options: 'ENGINE=InnoDB DEFAULT CHARSET=utf8')
```

## 複数のカラムを削除(remove_columns)
### 説明
指定したテーブルの複数のカラムを削除

### 使い方
```ruby
remove_columns(テーブル名, カラム名 [, ...])
```

### オプション

| オプション | 説明                          | デフォルト |
| :--------- | :---------------------------- | :--------- |
| :limit     | カラムの桁数を指定            |
| :default   | デフォルト値を指定            |
| :null      | nill値を許可するか            | true       |
| :precision | :decimal 型の精度を指定       |
| :scale     | :decimal 型の小数点以下の桁数 |

### 例
```ruby
remove_columns(:suppliers, :qualification, :experience)
```

## リファレンスの削除(remove_reference)
### 説明
既存のテーブルのリファレンスを削除する

### 使い方
```ruby
remove_reference(テーブル名, リファレンス名 [, オプション])
```

### オプション

| オプション   | 説明                   |
| :----------- | :--------------------- |
| :polymorphic | ポリモーフィックを付与 |
| :index       | インデックスを付与     |

### 例
オプションなし
```ruby
remove_reference(:products, :user, index: true)
```

オプションあり
```ruby
remove_reference(:products, :supplier, polymorphic: true)
```

## created_atとupdated_atの削除(remove_timestamps)
### 説明
既存のテーブルのcreated_atとupdated_atを削除する

### 使い方
```ruby
remove_timestamps(テーブル名)
```

### 例
usersテーブルのcreated_atとupdated_atを削除
```ruby
remove_timestamps(:users)
```

## インデックスの変更(rename_index)
### 説明
指定したテーブルのインデックスを変更する

### 使い方
```ruby
rename_index(テーブル名, 変更前の名前, 変更後の名前)
```

### 例
```ruby
rename_index :people, 'index_people_on_last_name', 'index_users_on_last_name'
```

## テーブルが存在するかチェック(table_exists?)
### 説明
テーブルが存在するかチェックする

### 使い方
```ruby
table_exists?(テーブル名)
```

### 例
```ruby
table_exists?(:developers)
```
