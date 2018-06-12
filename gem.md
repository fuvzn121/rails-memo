# Gem
## 必要なライブラリをインストール(bundle)
### 説明
RubyGemsの管理ツール

### コマンド一覧

| コマンド       | 説明                                             |
| :------------- | :----------------------------------------------- |
| bundle install | 依存ライブラリのインストール                     |
| bundle update  | 依存ライブラリのアップデート                     |
| bundle package | 依存ライブラリを「vender/cache」以下にまとめる   |
| bundle check   | 依存ライブラリがインストールされているかチェック |
| bundle list    | インストールされているライブラリの一覧           |
| bundle show    | gemファイルのソースのパスを表示                  |
| bundle init    | gemを初期化                                      |

### 例
依存関係のあるライブラリをインストール
```bash
$ bundle install
```

依存関係のあるライブラリをアップデート
```bash
$ bundle update
```

## Gemfile
### 説明
Railsで使用するGemの依存関係を管理するファイル

### 使い方
```gemfile
gem ライブラリ名 [, バージョン, オプション]
```

### バージョン

| バージョン         | 説明                                                                                         |
| :----------------- | :------------------------------------------------------------------------------------------- |
| x.x.x              | バージョンを固定                                                                             |
| a>= x.x.x          | x.x.x以上のバージョンが必要                                                                  |
| a>= x.x.x, < y.y.y | x.x.x以上、y.y.y以下のバージョンが必要                                                       |
| ~> x.0             | x.1からx.9は良いが、メインのバージョンがあがるとは不可<br>例えば、3.2は良いが、4.0は不可など |

### オプション

| オプション        | 説明                              |
| :---------------- | :-------------------------------- |
| :branch           | 対象となるブランチ                |
| :group or :groups | 環境(test/development/production) |
| :git              | gitレポジトリ                     |
| :require          | requireするgem                    |
| :platforms        | gemを利用するプラットフォーム     |
| :path             | gemファイルのディレクトリを指定   |

### 例

Rails3.2.1で固定

```gemfile
gem 'rails7, '3.2.1'
```

最新のRailsを使用

```gemfile
gem 'rails', :git => 'git://github.com/rails/rails.git'
```

### その他
初めに生成されるファイル例

```gemfile
source 'https://rubygems.org'

gem 'rails', '3.2.1'

gem 'sqlite3'

gem 'json'

group :assets do
  gem 'sass-rails',   '~> 3.2.3'
  gem 'coffee-rails', '~> 3.2.1'

  gem 'uglifier', '>= 1.0.3'
end
```

### source
gemで使用するライブラリが置いてあるURL

