# Gitレポジトリ
- 動かしてみたやつ
  https://github.com/itoo-mzn/Go/tree/master/src/opensearch

# 画面

- ダッシュボード
- DevTool（コンソール）

# コンポーネント

## index

- document の集合
- 操作
  - 一覧
    `GET _cat/indices`
  - とにかく全体の情報を大体確認したいとき
    `GET _search`
  - document の property を一覧
    下記の違いが理解できてないので、どれが正しいのかわからん。
    　`GET <index名> _mget`
    　`GET <index名>/_mapping`

## document

- 操作
  - 一覧
    ```
    GET <index名>/_search
    {
      "query": {
        "match_all": {}
      }
    }
    ```
  - 詳細（ID 指定で 1 件表示）
    `GET <index名>/_doc/<ID>`
  - 存在確認（bool で）
    `HEAD <index名>/_doc/<ID>`
  - 追加

  - 更新
    ```
    PUT <index名>/_doc/<ID>
    { "key": "val" }
    ```
  - 削除
    `DELETE <index名>/_doc/<ID>`

## Go client

- document
  - 追加
    - index
      追加。もし同じ ID の document があれば上書き。
      （document を index する。）
    - create
      追加。もし同じ ID の document があればエラー。作成専用。
  - 更新
    - update
