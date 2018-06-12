# Railsの基礎知識
## Ruby on Railsとは
- Ruby on Railsとは
  - Rubyにより構築されたWebアプリケーションフレームワーク
- 設計哲学
  - 設定より規約(CoC)
  - 同じ作業を繰り返さない(DRY)
- 特徴
  - MVCモデルを採用
  - ジェネレータ(scaffold)
  - アジャイルな開発に適している
  - ルーティング
  - テンプレート
  - データベースの管理方法
- 導入実績
  - クックパッド
  - 食べログ

## 規約
- ファイル名の規約
  - xxx : コントローラ名、モデル名
  - yyy : アクション名
  - mmm: マイグレーション名
  - YYYYMMDDhhmiss は作成日時が入る

|ディレクトリ|ファイル|クラス名|親クラス|
|:---|:---|:---|:---|
|app/controllers/|xxxs_controller.rb|XxxController|ApplicationController|
|app/models/|xxx.rb|Xxx|ActiveRecord::Base
|app/views/xxxs/|yyy.html.erb|||
|app/views/layouts/|xxx.html.erb|||
|app/helpers/|xxxs_helper.rb|||
|db/migrate/|YYYYMMDDhhmiss_mmm_xxxs.rb|MmmXxxs|ActiveRecord::Migration|
|test/fixtures/|xxx.yml|||

- テーブル定義についての規約
  - テーブル名とクラス名
    - テーブル名は複数形
    - 単語の区切りはアンダーバー(_)
    - 対応するクラス名は単語の先頭を大文字にして _ を取り除いたもの
  - キーのカラム名
    - 主キーのカラム名は「id」
    - 外部キーのカラム名は「テーブル名の単数_id」
  - 日付関連のカラム名
    - DATE型のカラムには名前を「受動態_on」
    - TIMESTAMP型のカラムには名前を「受動態_at」
    - 更新日時、作成日時は「updated_at」、「created_at」
  - 結合テーブル
    - 関連させたいテーブル名をくっつけた名前にする
    - カラム「id」を作らずに、関連させる2つのキーのセットを主キーにする
- Railsでのシングルクォーテーションとダブルクォーテーションの個人的な使い分け
  - コントローラやアクションの指定はシングルクォーテーション 
  - 上記以外はダブルクォーテーション
  - ただし、ダブルクォーテーション内はシングルクォーテーション

## フォルダ構造

|||説明|
|:---|:---|:---|
|Gemfile||gemの依存関係を指定できるファイル|
|README.rdoc||説明書|
|Rakefile|ターミナルから実行可能なタスク||
|config.ru||Rackの設定|
|app/||アプリケーションを格納するディレクトリ<br>主要なプログラムはこの配下に格納|
||assets/|スタイルシートや画像などを格納するディレクトリ|
||assets/images/|スタイルシートや画像などを格納するディレクトリ|
||assets/javascript/|公開するJavaScriptのスクリプトを格納するディレクトリ|
||assets/stylesheets/|公開するスタイルシートを格納するディレクトリ|
||controllers/|コントローラを格納するディレクトリ|
||controllers/application_controller.rb|アプリケーションで共通のコントローラ|
||helpers/|ヘルパーを格納するディレクトリ|
||helpers/application_controller.rb|アプリケーションで共通のヘルパー|
||models/|モデルを格納するディレクトリ|
||view/|ビューを格納するディレクトリ|
||views/layouts/|ビューのレイアウトとして使用するRHTMLテンプレートを格納するディレクトリ|
||views/layouts/application.html.erb|アプリケーションで共通のレイアウト|
|config/||プロジェクトの設定ファイルを格納するディレクトリ|
|config/environments/||環境単位の設定ファイルを格納するディレクトリ|
|config/initializers/||初期化ファイルを格納するディレクトリ|
|config/locales/||辞書ファイルを格納するディレクトリ|
|db/||データベースの設定ファイルを格納するディレクトリ|
||migrate/|マイグレーションファイルを格納するディレクトリ|
|doc/||ドキュメントを格納するディレクトリ|
|lib/||複数のアプリケーション間で共有するライブラリを格納するディレクトリ|
||assets/|自分で生成したライブラリを格納するディレクトリ|
||tasks/|自分で生成したRakefileを格納するディレクトリ|
|log/||ログファイルが格納されるディレクトリ。ログファイルはアプリケーションと環境ごとに作成される|
|public/||Web上に公開するファイルを格納するディレクトリ|
|script/||開発に役立つプログラムを格納されるディレクトリ|
||about|Rubyのバージョン情報、アプリケーションで仕様されているRailsのコンポーネント、およびその他の設定情報を表示するスクリプト|
||breakpointer|ブレークポイントが設定されたアプリケーションと通信しながら、アプリケーションの動作状況を対話的に調査するクライアントスクリプト|
||consoil|irbを使ってアプリケーションのメソッドを対話的に実行できるスクリプト|
||destroy|generateによって生成されたファイルを削除するスクリプト|
||generate|コードジェネレータ|
||plugin|pluginスクリプトにより、Railsの機能を拡張するプラグインのインストールと管理を行うスクリプト|
||runner|アプリケーション内のメソッドをWebコンテント外で実行するスクリプト|
||server|Webサーバ上でアプリケーションを実行するスクリプト|
||benchmarker|アプリケーション内の１つまたは複数のメソッドのパフォーマンス値を算出するスクリプト|
||profiler|アプリケーション内のコードを対象に、実行時にプロファイルの要約を生成するスクリプト|
|tmp/||キャッシュなど、一時的なファイルを格納されるディレクトリ|
|test/||アプリケーションのテストに使うファイルを格納するディレクトリ|
|vendor/||ライブラリや他のアプリケーションで共有するような外部ライブラリを格納するディレクトリ|
||rails/|rails:freeze:gemsタスクでバージョンを固定したRailsを格納するディレクトリ|
||plugins/|プラグインを格納するディレクトリ|

## アプリケーション作成の流れ
1. 作業ディレクトリの作成
```bash
$ mkdir rails
$ cd rails
```
2. アプリケーション作成
```bash
$ rails new demo
```
3. ディレクトリ移動
```bash
$ cd demo
```
4. 必要なgemのインストール
```bash
$ bundle install
```
5. データベースの設定
```bash
$ vi config/database.yml
```
6. データベースの作成
```bash
$ rake db:create
```
7. ジェネレータ
```bash
$ rails generate controller Say Hello goodbye
```
8. テーブル作成
```bash
$ rake db:migrate
```
9. サーバ起動
```bash
$ rails server
```

## Railsの実行環境
- 実行するときの3つの実行環境
  - development
  - test
  - production
- development
  - 開発中に使用する環境
  - 特徴
    - 実行環境の指定がなければこの環境で起動
    - ログレベルはdebug
    - 書き換えた内容が直ぐに反映
    - キャッシュが無効
- test
  - 自動テストで使用する環境
  - 特徴
    - ログレベルはdebug
    - キャッシュが有効
- production
  - 本番稼働で使用する環境
  - 特徴
    - ログレベルはinfo
    - キャッシュが有効
    - 書き換えた内容の反映には、再起動が必要
