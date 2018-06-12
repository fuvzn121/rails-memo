# Rake
## マイグレーションの実行(rake db:migrate)
### 説明
未実行のマイグレーションファイルを実行

### 使い方
```bash
$ rake db:migrate [VERSION=バージョン番号] [オプション]
```
### 実行の流れ
1. rake db:migrateを実行
2. schema_migrationsテーブルを調べ、存在しなければ作成
3. db/migrateディレクトリ内のすべてのマイグレーションファイルを調べる
4. データベースの現在のバージョンと異なるバージョンがあった場合、データベースに適応
5. schema_migrationsテーブルの更新

### 詳細

| コマンド                                              | 説明                                                       |
| :---------------------------------------------------- | :--------------------------------------------------------- |
| rake db:abort_if_pending_migrations                   | 実行されていないmigrationを表示                            |
| rake db:migrate [VERSION=バージョン番号] [オプション] | db/migrate内のスクリプトファイルからdatabaseにテーブル作成 |
| rake db:migrate:down                                  | 指定したmigrationファイルのself.downメソッドを実行         |
| rake db:migrate:redo [STEP=ステップ数]                | 指定したmigrationファイルのself.downメソッドを実行         |
| rake db:migrate:reset                                 | databaseを一度削除してもう一度作成し、db:migrate実行       |
| rake db:mgrate:up                                     | 指定したmigrationファイルのself.upメソッドを実行           |

### オプション

| オプション | ### 説明                                           | デフォルト  |
| :--------- | :--------------------------------------------- | :---------- |
| RAILS_ENV  | testやproduction環境の設定を使用する場合に使用 | development |
| VERBOSE    | 途中結果を表示するか                           | false       |

### 例

基本形(オプションなし)
```bash
$ rake db:migrate
```

プロダクション環境のマイグレーション
```bash
$ rake db:migrate RAILS_ENV=production
```

テスト環境のマイグレーション
```bash
$ rake db:migrate RAILS_ENV=test
```

特定のバージョンのスキーマに変更
```bash
$ rake db:migrate VERSION=201010190000
```

テーブルの初期化
```bash
$ rake db:migrate:reset
```

一つ前のバージョンに戻す
```bash
$ rake db:migrate:redo STEP=1
```

指定したマイグレーションのみ実行
```bash
$ rake db:migrate:up VERSION=201010190000
```

スキーマのバージョンを調べる
```bash
$ rake db:version
```

## マイグレーションをロールバック(rake db:rollback)
### 説明
マイグレーションを前のバージョンに戻す

### 使い方
```bash
$ rake db:rollback
```

### 例
基本形(オプションなし)
```bash
$ rake db:rollback
```

３つ前にロールバック
```bash
$ rake db:rollback STEP=3
```

## データベースに初期データを投入(rake db:seed)
### 説明
データベースに初期データを投入する。

### 使い方
```bash
$ rake db:seed
```

### 書き方
１件ずつ記述
```ruby
# db/seeds.rb
Category.create(:name => "Railsの基礎知識", :position => 1)
Category.create(:name => "Rubyの基礎知識", :position => 2)
```

まとめて記述
```ruby
# db/seeds.rb
5.times do |i|
     Page.create(:name => "テスト #{i}", :category_id => 1)
end
```

## Rakeとは
### Rakeとは
Rubyで記述されたビルドツールです。

## コマンド一覧(rake -T)
### 説明
Railsで使用できるコマンドの一覧を表示

### 使い方
```bash
$ rake -T
```

### 例
```bash
$ rake -T
rake about                              # List versions of all Rails frameworks and the environment
rake assets:clean[keep]                 # Remove old compiled assets
rake assets:clobber                     # Remove compiled assets
rake assets:environment                 # Load asset compile environment
rake assets:precompile                  # Compile all the assets named in config.assets.precompile
rake cache_digests:dependencies         # Lookup first-level dependencies for TEMPLATE (like messages/show or comments/_comment.html)
rake cache_digests:nested_dependencies  # Lookup nested dependencies for TEMPLATE (like messages/show or comments/_comment.html)
rake db:create                          # Creates the database from DATABASE_URL or config/database.yml for the current RAILS_ENV (use db:create:all to create all databases in the config)
rake db:drop                            # Drops the database from DATABASE_URL or config/database.yml for the current RAILS_ENV (use db:drop:all to drop all databases in the config)
rake db:fixtures:load                   # Load fixtures into the current environment's database
rake db:migrate                         # Migrate the database (options: VERSION=x, VERBOSE=false, SCOPE=blog)
rake db:migrate:status                  # Display status of migrations
rake db:rollback                        # Rolls the schema back to the previous version (specify steps w/ STEP=n)
rake db:schema:cache:clear              # Clear a db/schema_cache.dump file
rake db:schema:cache:dump               # Create a db/schema_cache.dump file
rake db:schema:dump                     # Create a db/schema.rb file that is portable against any DB supported by AR
rake db:schema:load                     # Load a schema.rb file into the database
rake db:seed                            # Load the seed data from db/seeds.rb
rake db:setup                           # Create the database, load the schema, and initialize with the seed data (use db:reset to also drop the database first)
rake db:structure:dump                  # Dump the database structure to db/structure.sql
rake db:structure:load                  # Recreate the databases from the structure.sql file
rake db:version                         # Retrieves the current schema version number
rake doc:app                            # Generate docs for the app -- also available doc:rails, doc:guides (options: TEMPLATE=/rdoc-template.rb, TITLE="Custom Title")
rake log:clear                          # Truncates all *.log files in log/ to zero bytes (specify which logs with LOGS=test,development)
rake middleware                         # Prints out your Rack middleware stack
rake notes                              # Enumerate all annotations (use notes:optimize, :fixme, :todo for focus)
rake notes:custom                       # Enumerate a custom annotation, specify with ANNOTATION=CUSTOM
rake rails:template                     # Applies the template supplied by LOCATION=(/path/to/template) or URL
rake rails:update                       # Update configs and some other initially generated files (or use just update:configs or update:bin)
rake routes                             # Print out all defined routes in match order, with names
rake secret                             # Generate a cryptographically secure secret key (this is typically used to generate a secret for cookie sessions)
rake stats                              # Report code statistics (KLOCs, etc) from the application or engine
rake test                               # Runs all tests in test folder
rake test:all                           # Run tests quickly by merging all types and not resetting db
rake test:all:db                        # Run tests quickly, but also reset db
rake test:db                            # Run tests quickly, but also reset db
rake time:zones:all                     # Displays all time zones, also available: time:zones:us, time:zones:local -- filter with OFFSET parameter, e.g., OFFSET=-6
rake tmp:clear                          # Clear session, cache, and socket files from tmp/ (narrow w/ tmp:sessions:clear, tmp:cache:clear, tmp:sockets:clear)
rake tmp:create                         # Creates tmp directories for sessions, cache, sockets, and pids
```

## 使用しているライブラリのバージョンを確認(rake about)
### 説明
使用しているライブラリのバージョンを確認

### 使い方
```bash
$ rake about
```

### 例
```bash
$ rake about
About your application's environment
Rails version             4.2.1
Ruby version              2.1.4-p265
RubyGems version          2.4.6
Rack version              1.5
JavaScript Runtime        JavaScriptCore
Middleware                Rack::Sendfile, ...
Application root          ...
Environment               development
Database adapter          sqlite3
Database schema version   0
```

## ソースコードからドキュメントを生成(rake doc:app)
### 説明
決められた記述で書かれたコメントやクラス定義からドキュメントを生成する。生成したドキュメントは、/doc/app/indec/htmlからアクセスする。

### 使い方
```bash
$ rake doc:app
```

### 例
```bash
$ rake doc:app
rm -r doc/app
Parsing sources...
100% [ 3/ 3]  app/helpers/application_helper.rb

Generating Darkfish format into /xxx/rails/xxx/doc/app...

Files:      3

Classes:    1 (1 undocumented)
Modules:    1 (1 undocumented)
Constants:  0 (0 undocumented)
Attributes: 0 (0 undocumented)
Methods:    0 (0 undocumented)

Total:      2 (2 undocumented)
  0.00% documented

Elapsed: 0.3s
```

## Railsのドキュメントを生成(rake doc:rails)
### 説明
Railsのドキュメントを生成

### 使い方
```bash
$ rake doc.rails
```

### 例
基本形(オプションなし)
```bash
$ rake doc.rails
```

## ソースコードにTODOを記入(rake notes)
### 説明
ソースコードに記入された「FIXME, OPTIMIZE, TODO」を検索して表示

### 使い方
```bash
$ rake notes
```

### 例
ソースコードにやり残しを記述

```ruby
def test
# TODO: やり残し
end
```
```bash
$ rake notes
  * [  3] [TODO] やり残し
```

## Railsのバージョンアップ(rake rails:update)
### 説明
Railsのバージョンアップ

### 使い方
```bash
$ rake rails:update
```

### 例
基本形(オプションなし)
```bash
$ rake rails:update
```

## 自動生成されるテンプレートをカスタマイズ(rake rails:templates:copy）
### 説明
自動生成されるテンプレートをカスタマイズ

### 使い方
```bash
$ rake rails:templates:copy
```

### 例
基本形(オプションなし)
```bash
$ rake rails:templates:copy
```

## Rakeファイルを自作
Rakeファイルは自作することもできる

## ログファイルを削除(rake log:clear)
### 説明
logフォルダ以下にある、ログファイルを削除する

### 使い方
```bash
$ rake log:clear
```

### 例
基本形(オプションなし)
```
$ rake log:clear
```

## データベースを作成(rake db:create)
### 説明
datebase.ymlの設定に従って、データベースを作成する。

### 使い方
環境ごと
```bash
$ rake db:create [RAILS_ENV=環境(development, text, production)]
```

すべて
```bash
$ rake db:create:all
```

### 例
基本形(オプションなし)
```bash
$ rake db:create
```

## データベースを削除(rake db:drop)
### 説明
datebase.ymlの設定に従って、データベースを削除する。

### 使い方
環境ごと
```bash
$ rake db:drop [RAILS_ENV=環境(development, text, production)]
```

すべて
```bash
$ rake db:drop:all
```

### 例
基本的な使い方
```bash
$ rake db:drop
```

production環境のデータベースを削除
```bash
$ rake db:drop RAILS_ENV=production
```

## マイグレーションの履歴(rake db:migrate:status)
### 説明
マイグレーションの履歴を表示する

### 使い方
```bash
$ rake db:migrate:status [RAILS_ENV=環境(development, text, production)]
```

### 例
基本形(オプションなし)

```bash
$ rake db:migrate:status

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20110521181506  Create pages
   up     20110521182915  Create categories
   up     20110703120321  Add position to pages
   up     20110716180121  Add position to categories
  down  20110724110158  Add english name to category
```

## マイグレーションのバージョンを確認(rake db:version)
### 説明
マイグレーションのバージョンを表示する

### 使い方
```bash
$ rake db:version [RAILS_ENV=環境(development, text, production)]
```

### 例
基本形(オプションなし)
```bash
$ rake db:version
Current version: 20110716180121
```

## スキーマファイルでデータベースを作成(rake db:schema:load)
### 説明

スキーマファイルでデータベースを作成する

### 使い方

$ rake db:schema:load [RAILS_ENV=環境(development, text, production)]
### 例

基本形(オプションなし)
```bash
$ rake db:schema:load
```

## 現在のデータベースからスキーマファイルを生成(rake db:schema:dump)
### 説明

現在のデータベースからスキーマファイルを生成する

### 使い方
```
$ rake db:schema:dump [RAILS_ENV=環境(development, text, production)]
```

### 例

基本形(オプションなし)
```bash
$ rake db:schema:dump
```

## データベースに初期データを挿入(rake db:seed)
### 説明

シードファイルを使ってデータベースに初期データを挿入する

### 使い方
```bash
$ rake db:seed [RAILS_ENV=環境(development, text, production)]
```

### 例
基本的な使い方
```bash
$ rake db:seed
```

production環境のデータベースにデータを挿入
```bash
$ rake db:seed RAILS_ENV=production
```

## データベースにテストデータを挿入(rake db:fixtures:load)
### 説明

フィクスチャファイルを使って、データベースにテストデータを挿入する

### 使い方
```bash
$ rake db:fixtures:load [FIXTURES=フィクスチャファイル名 RAILS_ENV=環境]
```

### 例

基本形(オプションなし)
```bash
$ rake db:fixtures:load
```
