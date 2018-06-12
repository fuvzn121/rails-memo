# railsコマンド(rails)
## アプリケーションの作成(rails new)
## 説明
アプリケーションに最低限必要なフォルダやファイルを自動的に作成

## 使い方
```bash
$ rails new アプリケーション名 [オプション]
```

### オプション

| オプション                  | 説明                                       | デフォルト |
| :-------------------------- | :----------------------------------------- | :--------- |
| -r, -ruby=PATH              | rubyバイナリのパス                         |
| -m, -template=TAMPLATE      | テンプレートのパス                         |            |
| --skip-gemfile              | Grmfileを作成しない                        |
| ｰB, --skip-bundle           | bundle installを行わない                   |
| -G, --skip-git              | .gitignoreを組み込まない                   |
| --skip-keeps                | .keepを組み込まない                        |
| -O, --skip-active-recode    | active recordを組み込まない                |
| -S, --skip-sprockets        | sprocketsを組み込まない                    |
| --skip-spring               | springアプリケーションをインストールしない |
| -d, --database=DATABASE     | データベースの種類                         | sqlite3    |
| -j, --javascript=JAVASCRIPT | 組み込むJavaScriptライブラリーを指定。     | jquery     |
| -J, --skip-javascript       | javascriptを組み込まない                   |
| --dev	github                | リポジトリ上の自分のコードから作成         |
| --edge                      | github リポジトリ上の最新のコードから作成  |
| -T, --skip-test-unit        | test::unitを組み込まない                   |
| --rc=RC                     |
| --no-rc                     |
| -f, --force                 | ファイルが存在する場合に上書きする         |
| -p, --pretend               | ドライラン                                 |
| -q, --quiet                 | 進捗情報を表示しない                       |
| -s, --skip                  | 既に存在するファイルについてはスキップ     |
| -h, --help                  | ヘルプ                                     |
| -v, --version               | バージョンを表示                           |

### 例
アプリケーションを作成
```bash
$ rails new weblog
```
mysqlを使うアプリケーションを作成
```bash
$ rails new weblog -d mysql
```
古いバージョンのRailsでアプリケーションを作成
```bash
$ rails _3.2.13_ new weblog
```

## モデルの生成(rails generate model)
### 説明
モデルを生成

### 使い方
```bash
$ rails generate model 名前 [カラム名:型] [オプション]
```

### オプション

| オプション                     | 説明                                   | デフォルト    |
| :----------------------------- | :------------------------------------- | :------------ |
| --skip-namespace               | 名前空間をスキップする                 |
| --old-style-hash               | 古いハッシュの形式を使う               |
| -o, -orm=名前                  | 使用するO/Rマッパーを指定              | active_record |
| --migration                    | マイグレーションファイルを生成するか   | true          |
| --timestamps                   | true                                   |
| --parent=名前                  |
| --indexes                      | true                                   |
| -t, --test-frameword=名前      | 使用するテストフレームワークを指定     | test_unit     |
| --fixtures                     | フィクスチャを生成するか               | true          |
| -r, --fixture-replacement=名前 | フィクスチャを変更する                 |               |
| -f, --force                    | ファイルが存在する場合に上書きする     |
| -q, --quiet                    | 進捗状況を表示しない                   |
| -p, --pretend                  | ドライラン                             |
| -s, --skip                     | 既に存在するファイルについてはスキップ |
| -h, --help                     | ヘルプを表示                           |

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

userモデルの作成
```bash
$ rails generate model user
      invoke  active_record
      create    db/migrate/YYYYMMDDHHMMSS_create_users.rb
      create    app/models/user.rb
      invoke    test_unit
      create      test/unit/user_test.rb
      create      test/fixtures/users.yml
```

## マイグレーションの生成(rails generate migration)
### 説明
マイグレーションファイル(テーブル定義の作成・変更を行うファイル)を生成

### 特徴
- 必ずupメソッドとdownメソッドを含めなければならない
- self.upがmigrationのバージョンがあがるときに実行
- self.downがmigrationのバージョンがあがるときに実行
- クラス名をすべて小文字にしたものが、ファイル名アンダースコア(_)以降と一致する必要がある

### 使い方
```bash
$ rails generate migration 名前 [カラム名:型]  [オプション]
```

### オプション

| オプション       | 説明                                   | デフォルト    |
| :--------------- | :------------------------------------- | :------------ |
| --skip-namespace | 名前空間をスキップする                 |               |
| --old-style-hash | 古いハッシュの形式を使う               |               |
| -o, -orm=名前    | 使用するO/Rマッパーを指定              | active_record |
| -f, --force      | ファイルが存在する場合に上書きする     |
| -q, --quiet      | 進捗状況を表示しない                   |
| -p, --pretend    | ドライラン                             |
| -s, --skip       | 既に存在するファイルについてはスキップ |
| -h, --help       | ヘルプを表示                           |

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

### 作成されるファイルの基本構成
```ruby
class マイグレーション名s < ActiveRecord::Migration
  def up
  end

  def down
  end
end
```

### 例
基本形(オプションなし)
```bash
$ rails generate migration Page
      invoke  active_record
      create    db/migrate/20120421134507_page.rb
```

カラムを指定して生成
```bash
$ rails generate migration AddTitleToPage title:string
      invoke  active_record
      create    db/migrate/20120421134409_add_title_to_page.rb
```

## ローカルでサーバを起動(rails server)
### 説明
Railsに付随しているWEBrickをサーバとして起動

### 使い方
```bash
$ rails server [オプション]
```

### オプション

| オプション             | 説明                                                    | 初期値              |
| :--------------------- | :------------------------------------------------------ | :------------------ |
| -p, --port=port        | サーバを起動するときのポート番号を指定                  | 3000                |
| -b, --binding=ip       | バインドするIPアドレスを指定                            | 0.0.0.0             |
| -c, --config=file      | rackupファイルを指定                                    |
| -d, --daemon           | デーモンとしてサーバを起動                              |
| -u, --debugger         | デバックモード                                          |
| -e, --environment=name | 環境(test/development/production)を指定してサーバを起動 | development         |
| -P, --pid=pid          | PIDファイルを指定                                       | tmp/pids/server.pid |
| -h, --help             | ヘルプを表示                                            |

### 例

開用WEBサーバを起動
```bash
$ rails server
=> Booting WEBrick
=> Rails 3.0.7 application starting in development on http://0.0.0.0:3000
=> Call with -d to detach
=> Ctrl-C to shutdown server
```

ポート番号を変更
```bash
$ rails server --p=3001
```

デーモンとして起動
```bash
$ rails server --d
```

本番として起動
```bash
$ rails server -e production
```

## プラグインをインストール(rails plugin install)
### 説明
プラグインをインストール

### 使い方
```bash
$ rails plugin install [プラグイン名/githubのURL] [オプション]
```

### オプション

| オプション      | 説明                                            |
| :-------------- | :---------------------------------------------- |
| -x, --externals | プラグインを取得するsvnを指定                   |
| -o, --checkout  | プラグインを取得するsvn checkoutを指定          |
| -e, --export    | プラグインを取得するsvn exportを指定            |
| -q, --quiet     | 進捗状況を表示しない                            |
| -r, --revision  | REVISION	チェックアウトするリビジョン番号を指定 |
| -f, --force     | ファイルが存在する場合に上書きする              |
| -h, --help      | ヘルプを表示                                    |

### 例
プラグインをインストール
```bash
$ rails plugin install continuous_builder asset_timestamping
```

## 自動生成したファイルの削除(rails destroy)
### 説明
rails generateで自動生成したファイルを削除

### 使い方
```bash
$ rails destroy 生成したファイルの種類 [削除するファイル名] [オプション]
```

###生成したファイルの種類
- controller
- generator
- helper
- integration_test
- mailer
- migration
- model
- observer
- performance_test
- plugin
- resource
- scaffold
- scaffold_controller
- session_migration
- stylesheets

### オプション

| オプション    | 説明                                   |
| :------------ | :------------------------------------- |
| -h, --help    | ヘルプを表示                           |
| -p, --pretend | ドライラン                             |
| -f, --force   | ファイルが存在する場合に上書きする     |
| -s, --skip    | 既に存在するファイルについてはスキップ |
| -q, --quiet   | 進捗状況を表示しない                   |

### 例
helloのコントローラを削除
```bash
$ rails destroy controller hello
```

マイグレーションファイルの削除
```bash
$ rails destroy migration AddSslFlag
   notempty  db/migrate
   notempty  db
         rm  db/migrate/20101030171223_add_ssl_flag.rb
```

プラグインをインストール
```bash
$ rails plugin remove continuous_builder
```

## アプリケーションに必要なコントローラ、モデル、ビューをまとめて生成(rails generate scaffold)
### 説明
アプリケーションの基本的な機能の一覧(index)、詳細(show)、新規作成(new/create)、編集(edit/update)、削除(destroy)を行うために必要なコントローラ、モデル、ビューをまとめて生成

### 使い方
```bash
$ rails generate scaffold 名前 [カラム名:型]
```

### オプション

| オプション                  | 説明                                                       |
| :-------------------------- | :--------------------------------------------------------- |
| -r, -ruby=PATH              | rubyバイナリのパス                                         |
| -b, --builder-BUILDER       | builderのパスを指定                                        |
| -m, -template=TAMPLATE      | テンプレートのパス                                         |
| --skip-gemfile              | Grmfileを作成しない                                        |
| --skip-bundle               | bundle installを行わない                                   |
| -G, --skip-git              | .gitignore, .gitkeepを組み込まない                         |
| -O, --skip-active-recode    | active recordを組み込まない                                |
| -S, --skip-sprockets        | sprocketsファイルをスキップ                                |
| -d, --database=DATABASE     | データベースの種類                                         |
| -j, --javascript=JAVASCRIPT | 組み込むJavascriptライブラリーを指定。デフォルトは、jquery |
| -J, --skip-javascript       | javaScriptを組み込まない                                   |
| --dev                       | github リポジトリ上の自分のコードから作成                  |
| --edge                      | github リポジトリ上の最新のコードから作成                  |
| -T, --skip-test-unit        | test::unitを組み込まない                                   |
| --old-style-hash            | 古いハッシュ形式(:foo => 'bar')を有効にする(Ruby1.9以上)   |
| -f, --force                 | ファイルが存在する場合に上書きする                         |
| -p, --pretend               | ドライラン                                                 |
| -q, --quiet                 | 進捗情報を表示しない                                       |
| -s, --skip                  | 既に存在するファイルについてはスキップ                     |
| -h, --help                  | ヘルプ                                                     |
| -v, --version               | バージョンを表示                                           |

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

### 生成されるファイル

| ファイル                                  | 説明                             |
| :---------------------------------------- | :------------------------------- |
| db/migrate/YYYYMMDDHHMMSS_create_XXXs.rb  | マイグレーションファイル         |
| app/assets/javascripts/XXXs.js.coffee     | モデル固有のCoffeeScript         |
| app/assets/stylesheets/XXXs.css.scss      | モデル固有のSCSSスタイルシート   |
| app/assets/stylesheets/scaffolds.css.scss | Scaffold共通のSCSSスタイルシート |
| app/controllers/XXXs_controller.rb        | コントローラファイル             |
| app/views/XXXs/index.html.erb             | すべてのリストを表示             |
| app/views/XXXs/edit.html.erb              | 編集ファイル                     |
| app/views/XXXs/show.html.erb              | 詳細ページ                       |
| app/views/XXXs/new.html.erb               | 新規ページ                       |
| app/views/XXXs/_form.html.erb             | フォーム用ページ                 |
| app/models/XXX.rb                         | モデルファイル                   |
| app/helpers/XXXs_helper.rb                | ヘルパー                         |
| test/functional/XXXs_controller_test.rb   | コントローラ用テストファイル     |
| test/unit/XXX_test.rb                     | モデル用テストファイル           |
| test/fixtures/XXXs.yml                    | fixtureファイル                  |
| test/unit/helpers/XXXs_helper_test.rb     | テスト用                         |
| public/stylesheets/scaffold.css           | デフォルトのスタイルシート       |

### 例
```bash
$ rails generate scaffold page name:string title:string
      invoke  active_record
      create    db/migrate/YYYYMMDDHHMMSS_create_pages.rb
      create    app/models/page.rb
      invoke    test_unit
      create      test/unit/page_test.rb
      create      test/fixtures/pages.yml
       route  resources :pages
      invoke  scaffold_controller
      create    app/controllers/pages_controller.rb
      invoke    erb
      create      app/views/pages
      create      app/views/pages/index.html.erb
      create      app/views/pages/edit.html.erb
      create      app/views/pages/show.html.erb
      create      app/views/pages/new.html.erb
      create      app/views/pages/_form.html.erb
      invoke    test_unit
      create      test/functional/pages_controller_test.rb
      invoke    helper
      create      app/helpers/pages_helper.rb
      invoke      test_unit
      create        test/unit/helpers/pages_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/pages.js.coffee
      invoke    scss
      create      app/assets/stylesheets/pages.css.scss
      invoke  scss
      create    app/assets/stylesheets/scaffolds.css.scss
```

## コントローラの生成(rails generate controller)
### 説明
コントローラとビューの生成

### 使い方
```bash
$ rails generate controller 名前 [アクション名...]
```

### オプション

| オプション                 | 説明                                   | 初期値    |
| :------------------------- | :------------------------------------- | :-------- |
| --skip-namespace           | 名前空間をスキップする                 |
| --skip-route               | config/routes.rbに追加しない           |
| -e, --template-engine=NAME | 使用するテンプレートエンジンを指定     | erb       |
| -t, --test-framework=NAME  | 使用するテストフレームワークを指定     | test_unit |
| --helper                   | ヘルパーを生成するか                   | true      |
| --assets                   | アセットを生成するか                   | true      |
| -f, --force                | ファイルが存在する場合に上書きする     |
| -p, --pretend              | ドライラン                             |
| -q, --quiet                | 進捗状況を表示しない                   |
| -s, --skip                 | 既に存在するファイルについてはスキップ |
| -h, --help                 | ヘルプを表示                           |

### 例
基本形(オプションなし)
```bash
$ rails generate controller Page
      create  app/controllers/page_controller.rb
      invoke  erb
      create    app/views/page
      invoke  test_unit
      create    test/functional/page_controller_test.rb
      invoke  helper
      create    app/helpers/page_helper.rb
      invoke    test_unit
      create      test/unit/helpers/page_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/page.js.coffee
      invoke    scss
      create      app/assets/stylesheets/page.css.scss
```

アクションとビューも生成
```bash
$ rails generate controller page title
      create  app/controllers/page_controller.rb
       route  get "page/title"
      invoke  erb
      create    app/views/page
      create    app/views/page/title.html.erb
      invoke  test_unit
      create    test/functional/page_controller_test.rb
      invoke  helper
      create    app/helpers/page_helper.rb
      invoke    test_unit
      create      test/unit/helpers/page_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/page.js.coffee
      invoke    scss
      create      app/assets/stylesheets/page.css.scss
```

階層化されたコントローラを生成
```bash
$ rails generate controller 'admin/page'
      create  app/controllers/admin/page_controller.rb
      invoke  erb
      create    app/views/admin/page
      invoke  test_unit
      create    test/functional/admin/page_controller_test.rb
      invoke  helper
      create    app/helpers/admin/page_helper.rb
      invoke    test_unit
      create      test/unit/helpers/admin/page_helper_test.rb
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/admin/page.js.coffee
      invoke    scss
      create      app/assets/stylesheets/admin/page.css.scss
```

## コンソールを起動(rails console)
### 説明
コンソールを起動

### 使い方
```bash
$ rails console [環境(test/development/production)] [オプション]
```

### オプション

| オプション   | 説明                                           |
| :----------- | :--------------------------------------------- |
| -s, -sandbox | 終了時にデータベースに関する変更をロールバック |
| -debugger    | デバックモードで起動                           |
| -irb         | irb                                            |
| -h, --help   | ヘルプ                                         |

### 例
コンソール起動
```bash
$ rails console
Loading development environment (Rails x.x.x)
irb(main):001:0>
```

production環境でコンソール起動
```bash
$ rails console production
Loading production environment (Rails x.x.x)
irb(main):001:0>
```

コンソールでSQLの出力を表示
```bash
$ rails console
irb(main):001:0> ActiveRecord::Base.logger = Logger.new(STDOUT)
```

## データベースクライアントを起動(rails dbconsole)
### 説明
コンソールを起動

### 使い方
```bash
$ rails dbconsole [環境(development, text, production)]
```

### 例
基本的な使い方
```bash
$ rails dbconsole
```

## Rails環境で動かすバッチ処理(rails runner)
### 説明
Rails環境で動かすバッチ処理

### 使い方
```bash
$ rails runner 実行するコード [オプション]
```

### オプション

| オプション | 説明                                     |
| :--------- | :--------------------------------------- |
| -e         | 環境((test/development/production)を指定 |
| -h, --help | ヘルプ                                   |
