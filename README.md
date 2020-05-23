# Dockerでリバースプロキシを構築するためのサンプル

## シナリオ
### 構成イメージ

- プロキシサーバ
* proxy
example1.com, example2.com => web1,web2へそれぞれ転送する
80,443でそれぞれ受け取り、web1,web2ではproxy 用のポートを開けておく

- Webサーバ(1)
* Web1
- example1.com

- Webサーバ(2)
* Web2
- example2.com

### 構築手順

1. proxy, web1, web2にてそれぞれDockerイメージをビルドする
```
docker-compose up -d
# 再ビルドが必要な場合
docker-compose build
```
2. proxy, web1, web2で使用するdockerのnetworkを構築する
```
docker network create proxy-web-link
```

3. テストするために、hosts (/etc/hosts)ファイルに記載する
```
# web1
127.0.0.1 example1.com
# web2
127.0.0.1 example2.com
```
4. example1.com, example2.com にそれぞれアクセスしhtmlが表示されるとOK