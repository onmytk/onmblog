---
title: "GitHub Pages + Hugoでブログ"
date: 2019-05-05T02:55:03+09:00
draft: false 
categories: [ "web" ]
tags: [ "github", "hugo" ]
---

## Hugoとは
[Hugoとは](https://www.google.co.jp/search?q=Hugo)

## GitHub Pagesとは
[GitHub Pagesとは](https://www.google.co.jp/search?q=GitHub+Pages)

## 手順
### 環境
* Ubuntu 16.0.4

### Hugoインストール
```sh
$ sudo apt-get install hugo
```
### GitHubリポジトリ作成
GitHub Pagesを公開するリポジトリを作成する。
GitHub PagesのURLは次のようになる。  
`https://<ユーザ名>.github.io/<リポジトリ名>`

### サイトを作成
ホームディレクトリに作業用のblogディレクトリを作成する。`hugo new site <サイト名>`でサイトを作成する。
```sh
$ mkdir ~/blog
$ cd ~/blog
$ hugo new site <サイト名>
```

### Hugoのテーマ追加
[Hugo Themes](https://themes.gohugo.io/)からサイトのテーマを探す。テーマのDownloadをクリックするとGithubに飛ぶ。themesディレクトリに`git clone`をすることで追加する。
```sh
$ cd themes
$ git clone <git url>
```

### Hugoの設定
config.tomlを適宜編集する。
```sh:config.toml
theme = "<テーマ名>"
baseurl = "https://<ユーザ名>.github.io/<リポジトリ名>"
canonifyurls = true
```

### とりあえず記事作成
ページを作成する。
```sh
$ hugo new posts/<ページタイトル>.md
```

`~/blog/<サイト名>/content/posts/<ページタイトル>.md`が作成される。内容は以下の感じ。
```
---
title: "<ページタイトル>"
date: 2019-05-05T00:16:28+09:00
draft: true 
---

# test
## test

```
---で囲まれてる中がメタデータ？になる。`draft`は`true`だと下書き状態、`false`で公開となる。---以下が内容を書く。

### ビルド
ホスティング内容を生成する。
```sh
$ hugo
```
ホスティング内容が`public`ディレクトリ下に生成される。

### ローカルで確認
ローカルサーバを起動する。
```sh
$ hugo server -D
```
`localhost:1313/<リポジトリ名>`でプレビューを確認可能。


### 公開
`public`ディレクトリ下をgh-pagesブランチへpushする。
```sh
$ cd public
$ git init
$ git remote add origin git@github.com:<ユーザ名>/<リポジトリ>.git
$ git checkout -b gh-pages
$ git add .
$ git commit -m 'initial commit'
$ git push origin gh-pages
```

`baseurl`に設定したURLにアクセスすると公開される。

### その他
参考URLやHugoページを参照

## 参考
[HugoとGitHub Pagesで静的サイトを公開する](https://qiita.com/satzz/items/e24bd703fc04fb45f7ef)
[【2018年版】Hugoとgithub pagesでブログ作る方法【Circle CIも回します】](https://qiita.com/ryoma-tokushige/items/eba3e6cd415e9755af87)

[onmytk/onmblog](https://github.com/onmytk/onmblog)
