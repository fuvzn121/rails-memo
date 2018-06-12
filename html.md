# HTMLの基礎知識
## XHTMLの基礎
### XML宣言
使い方
```xml
<?xml version="1.0" encoding="UTF-8"?>
```
### 文章型宣言
使い方
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN""http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
### html要素
使い方
```html
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="ja" lang="ja">
```
### ページタイトル
使い方
```html
<title>サイト名</title>
```
例

トップページ
```html
<title>サイト名 - サイトの説明</title>
```
カテゴリトップ
```html
<title>カテゴリ名 | サイト名</title>
```
個別ページ
```html
<title>ページ名 | カテゴリ名 | サイト名</title>
```
### メタ情報
```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<meta http-equiv="Content-Style-Type" content="text/css" />
<meta http-equiv="Content-Script-Type" content="text/javascript" />
<meta name="description" content="ページの概要文" />
<meta name="keywords" content="キーワード" />
<meta name="author" content="制作者" />
<meta name="copyright" content="著作権保有者" />
```
### 文章間関係(link要素)
スタイルシートファイルの指定
```html
<link rel="stylesheet" type="text/css" href="css/import.css" media="screen, projection, tv" />
```
RSSファイルの指定
```html
<link rel="alternate" type="application/rss+xml" title="RSS 2.0" href="feed.xml" />
```
トップページやヘルプページの指定
```html
<link rel="contents" href="index.html" title="ホーム" />
<link rel="help" href="help.html" title="ヘルプ" />
```
日本語以外の言語で制作したページ
```html
<link rel="alternate" type="text/html" href="index-en.html" hreflang="en" />
```
スクリプト
```html
<script type="text/javascript" src="/javascripts/prototype.js">
```
### サイト所有者
```html
<address>Copyright &copy; 2009 サイト名. All Rights Reserved.</address>
```
### フォントの種類
```css
body, p, ol, ul, td {
  font-family:'ヒラギノ角ゴ Pro W3','Hiragino Kaku Gothic Pro','メイリオ', Meiryo,'ＭＳ Ｐゴシック', "MS P Gothic", sans-serif;
}
```

### 一般的なID名

| 機能・エリア                         | 命名例                                           |
| :----------------------------------- | :----------------------------------------------- |
| 本文全体を囲むボックス               | container, wrapper, page, pagebody, all          |
| ヘッダー                             | header, header-area                              |
| ナビゲーション                       | nav, navi, navigation                            |
| グローバルナビゲーション             | global-nav, gnav                                 |
| ローカルナビゲーション               | local-nav, lnav                                  |
| 補足ナビゲーション                   | assist-nav, utility, utility-nav                 |
| パンくずナビゲーション               | topicpath, breadcrumbs                           |
| コンテンツ全体                       | content(s), container, wrapper                   |
| メインコンテンツ                     | main, maincontent(s), content(s), alpha, primary |
| サブコンテンツやサイドバー           | sub, subcontent(s), sidebar, beta, secondary     |
| 見出しと本文のまとまり               | section, entrybody, article(s)                   |
| 記事単体                             | article(s), entry(-ies)                          |
| フッター                             | footer, footer-area, copyright, publication      |
| ロゴ                                 | logo                                             |
| キービジュアルやメインビジュアル     | keyvisual, mainvisual                            |
| 画像や写真、グラフなど               | image, photo, fig, figure                        |
| 検索                                 | search, search-area, search-box                  |
| ヒント、本題から外れた補足や囲み記事 | aside, hint, note                                |
| 商品一覧                             | products, item-list, shopitems                   |

### フォーム例
```html
<form action="" method="post">
  <p>説明</p>
  <fieldset>
    <legend>ラベル</legend>
    <dl id="customer">
      <dt><label for="name">名前</label></dt>
    <dd>
      <input type="radio" name="sex" id="man" /><label for="man">男性</label>
      <input type="radio" name="sex" id="woman" /><label for="woman">女性</label>
    </dd>
  </dl>
 </fieldset>
 <fieldset>
   <legend>評価</legend>
   <dl id="rating">
     <dt>項目</dt>
     <dd>
       <ul>
         <li>項目1</li>
         <li>項目2</li>
       </ul>
     </dd>
     <dt><label for="freetext">説明</label></dt>
     <dd><input type="text" size="50" id="freetext" /></dd>
   </dl>
 </fieldset>
 <div><input type="submit" value="確認" /></div>
</form>
```
### レイアウト例
1カラムレイアウト
```css
div#header
div#global-nav
div#container
div.article#new-entry
div.entry-header
div.entry-body
div.entry-footer
div#previous-entry
div.article
div.article
div.step-nav
div#other-contents
div.section-lv2#about
div.section-lv2#archives
div.section-lv2#category
div#footer
```
2カラムレイアウト
```css
div#global-nav
div#search
div#utility-nav
div.structure#container
div.section-lv1#primary-contents
div.section-lv2
div.section-lv2
div#secondary-contents
div.section-lv2#classroom
div.section-lv2
div.structure#footer
```
エラステリックレイアウト
```css
div#header
div#global-nav
div#lead
div#wrapper
div#content
div.highlight
div.highlight
div#aside
div#shortcut
div#feed
div#footer
```
プロパティの指定順序
```css
/* Suggested order
 * display
 * list-style
 * position
 * float
 * clear
 * width
 * height
 * margin
 * padding
 * border
 * background
 * color
 * font
 * text-decoration
 * text-align
 * vertical-align
 * white-space
 * other text
 * content
*/
```

1. 表示や配置など「視覚整形モデル」に関するプロパティ
2. マージンやパディング、ボーダーなど「ボックスモデル」に関するプロパティ
3. 背景と前景に関するプロパティ
4. フォントとテキストに関するプロパティ
5. 生成内容に関するプロパティ

## HTTPステータスコードとシンボル名

| コード | 名前                            | シンボル                         |
| :----- | :------------------------------ | :------------------------------- |
| 100    | Continue                        | :continue                        |
| 101    | Switching Protocols             | :switching_protocols             |
| 102    | Processing                      | :processing                      |
| 200    | OK                              | :ok                              |
| 201    | Created                         | :created                         |
| 202    | Accepted                        | :accepted                        |
| 203    | Non-Authoritative Information   | :non_authoritative_information   |
| 204    | No Content                      | :no_content                      |
| 205    | Reset Content                   | :reset_content                   |
| 206    | Partial Content                 | :partial_content                 |
| 207    | Multi-Status                    | :multi_status                    |
| 226    | IM Used                         | :im_used                         |
| 300    | Multiple Choices                | :multiple_choices                |
| 301    | Moved Permanently               | :moved_permanently               |
| 302    | Found                           | :found                           |
| 303    | See Other                       | :see_other                       |
| 304    | Not Modified                    | :not_modified                    |
| 305    | Use Proxy                       | :use_proxy                       |
| 306    | Reserved                        | :reserved                        |
| 307    | Temporary Redirect              | :temporary_redirect              |
| 400    | Bad Request                     | :bad_request                     |
| 401    | Unauthorized                    | :unauthorized                    |
| 402    | Payment Required                | :payment_required                |
| 403    | Forbidden                       | forbidden                        |
| 404    | Not Found                       | not_found                        |
| 405    | Method Not Allowed              | :method_not_allowed              |
| 406    | Not Acceptable                  | :not_acceptable                  |
| 407    | Proxy Authentication Required   | :proxy_authentication_required   |
| 408    | Request Timeout                 | :request_timeout                 |
| 409    | Conflict                        | :conflict                        |
| 410    | Gone                            | :gone                            |
| 411    | Length Required                 | :length_required                 |
| 412    | Precondition Failed             | :precondition_failed             |
| 413    | Request Entity Too Large        | :request_entity_too_large        |
| 414    | Request-URI Too Long            | :request_uri_too_long            |
| 415    | Unsupported Media Type          | :unsupported_media_type          |
| 416    | Requested Range Not Satisfiable | :requested_range_not_satisfiable |
| 417    | Expectation Failed              | :expectation_failed              |
| 422    | Unprocessable Entity            | :unprocessable_entity            |
| 423    | Locked                          | :locked                          |
| 424    | Failed Dependency               | :failed_dependency               |
| 426    | Upgrade Required                | :upgrade_required                |
| 500    | Internal Server Error           | :internal_server_error           |
| 501    | Not Implemented                 | :not_implemented                 |
| 502    | Bad Gateway                     | :bad_gateway                     |
| 503    | Service Unavailable             | :service_unavailable             |
| 504    | Gateway Timeout                 | :gateway_timeout                 |
| 505    | HTTP Version Not Supported      | :http_version_not_supported      |
| 506    | Variant Also Negotiates         | :variant_also_negotiates         |
| 507    | Insufficient Storage            | :insufficient_storage            |
| 510    | Not Extended                    | :not_extended                    |

MIMEタイプ
MEMEタイプとは

データ形式を表したもので、Webサーバとブラウザが通信するときにデータの種類を表すのに使われます。

主なMIMEタイプ

| MIMEタイプ                    | ファイルの種類           | 拡張子      |
| :---------------------------- | :----------------------- | :---------- |
| text/plain                    | プレーンティストファイル | .txt        |
| text/html                     | HTMLファイル             | .html, .htm |
| test/css                      | スタイルシーとファイル   | .css        |
| text/javascript               | JavaScriptファイル       | .js         |
| image/gif                     | GIFファイル              | .gif        |
| image/png                     | PNGファイル              | .png        |
| image/jpeg                    | JPEGファイル             | .jpg, .jpeg |
| video/mpeg                    | MPEGファイル             | .mpeg, .mpg |
| video/quicktime               | Quicktimeファイル        | .qt, .mov   |
| application/pdf               | PDFファイル              | .pdf        |
| application/msword            | ワードファイル           | .doc        |
| application/x-shockwave-flash | Flachファイル            | .swf        |
| application/zip               | zipファイル              | .zip        |

## 言語コード
### 言語コードとは
対象とする内容の言語を指定

### 主な言語コード

| 言語コード | 言語名       |
| :--------- | :----------- |
| ja         | 日本語       |
| en         | 英語         |
| de         | ドイツ語     |
| es         | スペイン語   |
| fr         | フランス語   |
| ko         | 韓国語       |
| zh         | 中国語       |
| pt         | ポルトガル語 |
| it         | イタリア語   |

## リンクタイプ
### リンクタイプとは
リンク先の役割

### リンクタイプ一覧
HTML4で定義済みのキーワード

| リンクタイプ | 内容                             |
| :----------- | :------------------------------- |
| alternate    | 代替にあたる文書                 |
| stylesheet   | 外部スタイルシート               |
| appendix     | 付属書にあたる文書               |
| bookmark     | 文書内の重要なアンカーへのリンク |
| contents     | 目次にあたる文書                 |
| copyright    | 著作権に関する記述のある文書     |
| glossary     | 指定する文書が用語集             |
| help         | ヘルプにあたる文書               |
| index        | 索引にあたる文書                 |
| next         | 次の文書                         |
| prev         | 前の文書                         |
| start        | 一連の文書の中で最初の文書       |
| chapter      | 一連の文書の中で章にあたる文書   |
| section      | 一連の文書の中で節にあたる文書   |
| subsection   | 一連の文書の中で項にあたる文書   |

HTML5で定義されるキーワード

| リンクタイプ | 内容                                                         |
| :----------- | :----------------------------------------------------------- |
| alternate    | 代替にあたる文書                                             |
| archives     | 過去のコンテンツを集めたアーカイブ                           |
| author       | 文書の制作者                                                 |
| bookmark     | 親にあたるセクション内のコンテンツのパーマリンク             |
| external     | リンク先が外部サイト                                         |
| first        | 初回のコンテンツとして参照されるべき文書                     |
| help         | 文書のヘルプ                                                 |
| icon         | サイトもしくはドキュメントのアイコン                         |
| index        | 文書の索引                                                   |
| last         | 最終回のコンテンツとして参照されるべき文書                   |
| license      | 著作権やライブラリ、ソフトウェア等の使用条件が記された文書   |
| next         | 次回のコンテンツとして参照されるべき文書                     |
| nofollow     | リンク先のコンテンツについては保証・責任がもてないコンテンツ |
| noreferrer   | HTTPリファラの欄を空白にしたまま送信                         |
| pingback     | リンク先にリンクを張ったことを自動的に通知                   |
| prefetch     | リンク先のリソースを事前にロード                             |
| prev         | 前回のコンテンツとして参照されるべき文書                     |
| search       | 検索機能がある文書                                           |
| stylesheet   | 外部スタイルシート                                           |
| sidebar      | 視覚環境のUAのサイドバー欄に表示                             |
| tag          | 文書のタグ                                                   |
| up           | 1つ上の階層の文書                                            |
