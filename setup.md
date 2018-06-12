# セットアップ
## Linuxへのインストール
### 作業用のディレクトリに移動
```bash
$ mkdir demo
$ cd demo
```
### Rubyのインストール
ブラウザからダウンロード
- [Rubyの公式サイト](http://www.ruby-lang.org/ja/)

ターミナルからダウンロード
```bash
$ wget "ftp://ftp.ruby-lang.org/pub/ruby/1.8/ruby-1.8.7-p302.tar.gz"
$ tar xzf ruby-1.8.7*tar.gz
$ cd ruby-1.8.7-*
$ ./configure
$ make
$ sudo make install
$ make clean
$ ruby -v
```

- インストールディレクトリを指定する場合
  ```bash
  ./configure --prefix=ディレクトリパス
  ```

### RubyGemsのインストール
RubyGemsとは
- Rubyの代表的なパッケージ管理システム

ブラウザからダウンロード
- [RubyForge RubyGems Project Info](http://rubyforge.org/projects/rubygems/)

ターミナルからダウンロード
```bash
$ wget http://rubyforge.org/frs/download.php/70696/rubygems-1.3.7.tgz
$ tar xzf rubygems-1.3.7.tgz
$ cd rubygems-1.3.7
$ ruby setup.rb
```

### Railsのインストール

最新バージョンをインストール
```bash
$ gem install rails
```

特定のバージョンのRailsをインストール
```bash
$ gem install rails -v 2.3.8
```

## Windowsへのインストール
WindowsへのインストールはRails Installerを使うのが簡単です。

## Rails Installer
### 説明
Railsに必要なソフトウエアをWindowsにまとめてインストールできるパッケージ

### インストール
[Rails Installer](http://railsinstaller.org/)

## Macへのインストール
MacへのインストールはRails Installerを使うのが簡単です。

## Rails Installer
### 説明
Railsに必要なソフトウエアをMacにまとめてインストールできるパッケージ

### インストール
[Rails Installer](http://railsinstaller.org/)
