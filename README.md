# k6-load-testing

## 負荷テスト基盤の起動

`docker-compose up -d`

## Grafanaの設定

### Grafanaにアクセス

`http://localhost:3000`

ログイン画面が表示されるのでログインする（初期アカウントはUsername, Password共に`admin`）

### データソースの追加

`Data Sources > Prometheus`

**Prometheus server URL**には`http://prometheus:9090`を設定し、"Save & Test"を押下

### ダッシュボード作成

`Dashboards`から[k6 Prometheus Dashboard](https://grafana.com/grafana/dashboards/19665-k6-prometheus/)をimportする

（ダッシュボードID: `19665`）


## 負荷テスト実行

```shell
docker compose run k6 -o experimental-prometheus-rw run /scripts/sample.js
```

## 負荷テスト用スクリプト作成 Tips

ローカルで起動しているアプリケーションに対して負荷テストを行う場合、`localhost`を`host.docker.internal`に置き換える。

```js
let res = http.get("http://host.docker.internal:8080");
```

## 参考資料

https://zenn.dev/nyama39/articles/3ef0d951e2aa30

https://zenn.dev/hal_shu_sato/articles/docker-compose-container-host-connection