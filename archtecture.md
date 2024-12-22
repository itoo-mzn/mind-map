- Web サーバー
- アプリケーションサーバー

  - 層の分け方

    - _3 層_
      3 層に分けて考えるが、
      1 つの実体が 2 つの層にまたがっている実体もある。
      Rails など[\*](https://www.kanzennirikaisita.com/posts/what-is-service-class)
      - _プレゼンテーション層_
        - 役割
          クライアントとやりとりする。
        - 実体
          - Controller
          - View
        - 例
          - 受け付ける型やレスポンスを定義。
          - 日付のフォーマット。
            （ただし日付フォーマットが主たる目的のアプリケーションの場合はビジネスロジック。）
          - API 定義に記載するレベルのバリデーション
            （これより複雑なルールならビジネスロジックにしていいのかと思う。）
      - _ビジネスロジック層_
        - 役割
          - ユースケースの実現
          - ビジネスロジック
            2 種類ある。
            - _エンタープライスビジネスルール_
              システム都合でないコアなルール。
            - _アプリケーションビジネスルール_
              　システムを成立させるためのロジック。（処理の流れやトランザクション管理など。）
          - （プレゼンテーション層でもデータアクセス層でもないもの[\*](https://qiita.com/os1ma/items/25725edfe3c2af93d735)）
        - 実体
          - Service
          - DTO
            など
      - _データアクセス層_
        - 役割
          どこかにあるデータを読み書きする。
        - 実体
          - Model
          - DAO
            など
    - レイヤード
    - ヘキサゴナル
    - オニオン

  - 各層の実装方式

    - MVC、MVVM、MVP

    - _ビジネスロジック層_
      サービス（サービスクラス）には 3 種類ある。[\*](https://www.kanzennirikaisita.com/posts/what-is-service-class)

      - _トランザクションスクリプトパターン_
        - Service クラス
          処理を記述。
          ユースケースの実現＋コアなルール
          （エンタープライスビジネスルール＋アプリケーションビジネスルール）
        - DTO
          データの入れ物とする。
          getter, setter だけを持つ。（処理は Service に。）
      - _ドメインモデルパターン_
        アプリケーション層とドメイン層 に分けたりもする。
        - DTO
          処理を持つ。
        - Service
          2 種類ある。
          - _アプリケーションサービス_（inDDD）、_ユースケース_（in クリーンアーキテクチャ）
            アプリケーションビジネスルール（処理の流れなど）を実現する。
          - （_ドメインサービス_）
            DDD におけるドメインモデル最後の手段。

    - _データアクセス層_
      大きく 5 種類。[\*](https://speakerdeck.com/recruitengineers/shi-jian-obuziekutozhi-xiang-she-ji-sabuzi-liao-detamoderuzhong-xin-she-ji?slide=3)[\*](https://hamasyou.com/blog/2004/10/28/daoor/)
      - DAO(Data Access Object)（= Table Data Gateway パターン）
        DB に接続する手段を隠蔽して、
        Select()や Update()などのメソッドを提供するもの。
      - Row Data Gateway パターン
      - Active Record パターン
        データへのアクセス機能とビジネスロジックを持つ。
      - O/R マッピング（= Data Mapper パターン）
        オブジェクトと DB データをマッピングする。
      - Repository[\*](https://zenn.dev/kohii/articles/e4f325ed011db8)

  - デザインパターン
    - Iterator

- DB サーバー

- 仮置き場
  - DTO(Data Transfer Object)
    データの受け渡し用のクラス。
    ビジネスロジックは持たない。
    プレゼンテーション層とビジネスロジック層の間で使う。
