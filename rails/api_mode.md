source
- https://railsguides.jp/api_app.html
何が書いてあった？
railsをAPI専用のアプリケーションとして使うための解説が書いてあった
- `bin/rails new my_api --my_api`
- ミドルウェアを絞り込んで起動
- ActionController::APIを継承
- ビュー、ヘルパー、アセットを生成しない設定になると
なんでrails でapiサーバーを作るのか？
- 過剰すぎないか？だけど理由がありますよ
理由
- ロジックの部分は結局view以外にあって、railsだったら細かな設定をしなくても素早くアプリケーションを立ち上げることができる
- パラメーター解析
  - JSONとかhtmlにエンコードされたデータを自動的に、Rubyのハッシュオブジェクトに変えることができる
- セキュリティ的にも優れてるよ
  - 詳しい話はなかった
- 透過的再読み込み
  - オートロード、railsの内部エンジンがかっこいい名前だった
- developmentモード
  - 開発用の環境、それこそオートロードが設定されてるモード
- test
  - ↑と同じ、テストしやすい（テストに使われる気がする）
- ログ出力
- 条件付きGET
  - ETag, last_modifiedとかをみて条件付きGETをやってくれる
	- `stale?`
- HEAd変換
  - headリクエストをgetと変換してくれるので、headリクエストが使用可能

Action Pack層で提供される機能（コントローラーやビューの処理を対応する部分のこと）
- リソースベースルーティング
  - httpからコントローラへの明確なマッピングを利用できる
- url生成
- ヘッダレスポンス、リダイレクトレスポンスの生成
  - head :no_contentとか
- キャッシュ
  - ページキャッシュ（ページを丸ごとキャッシュ、Nginxとかがhtmlを返す）
	- アクションキャッシュ(コントローラの処理の結果をキャッシュ)
	- フラグメントキャッシュ(ページまたはjsonの一部だけキャッシュする, APIで一番大事)
- 認証
  - ダイジェスト認証、basic認証、トークン認証
- ジェネレーター
- 計測（instrumentation）
- プラグイン（gem）

既存のアプリをAPI専用にする設定(config/application.rb)
- config.api_only = true
- 継承するベースをActionController::Apiに変える
- ログを出すようにするとか（デフォルトではhtml上に出るやつを、サーバーの標準出力に出す）

ピックアップされたmiddlewareの説明
- JSON形式のデータをエンコードしてくれるやつ
- Rack::Sendfile
- Rack::Cache
  - stale?メソッドを使う
	- gemをインストールして使う
	- memcacheを設定とか

- セッションミドルウェアの話
  - デフォルトではインストールされていない(ステートレス性、軽量化のため)
	- sessionを有効にするために、applicationの設定ファイルに追加しないといけない

middlewareを追加、削除する設定
- 設定ファイルに追加する
- config.middleware.use
- config.middleware.delete

ActionController::APIにはたくさんモジュールがインストールされてるよ
- Callbacks, Rendersとか



