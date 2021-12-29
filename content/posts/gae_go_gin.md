---
title: "GAE/Go + ginでAPIサーバを作る"
date: 2019-05-13T21:30:20+09:00
draft: true
categories: [ "web" ]
tags: ["GAE", "Go", "gin" ]
description: "サンプルアプリケーションの起動まで"
---

## Webアプリ概要
Todo

## 環境
- Ubuntu 18.10
- Go 1.10
- python 2.7.15

## 手順
### Google Cloud SDKのインストール
[Google Cloud SDKのドキュメント](https://cloud.google.com/sdk/docs/?hl=ja#deb)

```sh
$ gcloud init
```
でアカウントの設定、新しいプロジェクの作成まで行う。

```sh
$ sudo apt-get install google-cloud-sdk-app-engine-python google-cloud-sdk-app-engine-go google-cloud-sdk-datastore-emulator
```


### Google App Engineアプリケーションの作成
[Google Cloud Platform](https://console.cloud.google.com/)  
App Engine > 開始 >  
Language: Go  
Environment: 標準  
-> 作成

### GAE設定ファイル作成
```yaml:app.yaml
version: 1
runtime: go
api_version: go1

handlers:
- url: /.*
  script: _go_app
```

### サンプルアプリケーション

```go:main.go
package main

import (
	"net/http"
	"github.com/gin-gonic/gin"
)

func init()  {
	gin.SetMode(gin.ReleaseMode)
	r := gin.New()

	r.GET("/", func(c *gin.Context) {
		c.String(http.StatusOK, "Hello World")
	})

	r.GET("/ping", func(c *gin.Context)  {
		c.String(http.StatusOK, "pong")
	})

	http.Handle("/", r)
}
```

### サンプルアプリケーションの起動
```sh
$ dev_appserver.py app.yaml
```
localhost:8080にアクセスしてHello Worldが表示されてればおｋ


