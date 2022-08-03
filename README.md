# Go Architecture

## The Clean Architecture
<img width="727" alt="スクリーンショット 2022-08-02 8 07 55" src="https://user-images.githubusercontent.com/65061306/182260133-19be1a99-0285-46b8-af65-12577a9e1158.png">

https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html


## 分かりやすい解説動画
- https://www.youtube.com/watch?v=pbCRHAM5NG0

## メモ
- 制御の流れと依存の関係は分離して考える
- 変更頻度が高いオブジェクトは、依存される側より依存する側にすべし。何故なら、依存する側を修正しても依存される側には影響はない。しかし、依存される側を修正したら依存する側にも影響があるため。
- アプリケーションの本質的な価値を提供するオブジェクトは、依存されない側にすべし。

### entity
- データレコードを表現するクラス
- ドメインロジックを実装する責務を持つ．
- DB操作などの技術的な実装を持ってはならない．
- また，他のどのレイヤにも依存してはならない．
- オブジェクトでビジネスロジックを表現する責務

### repository
- データの集約、永続化の責務

### usecase
- 技術的な要素を省いた、ビジネスルール
- Entity・Repositoryを使い、ユースケースを達成する責務

### controler
- 外界からの入力を、達成するユースケースが求めるインタフェースに変換する責務
 
### FrameWorks & Drivers
- httpリクエストの受付
- DBとの接続
- ミドルウェアとの実際の接続や入出力などを担当するレイヤー

# go-architecture

## golang reccomend architecture

<pre>
.
├── main.go
├── go.mod
├── go.sum
|
├── cmd
└── lib
└── app
    └── app
    └── config
    └── domain
    |    └── entity
    |    └── repository
    └── ui  
    |    └── cli
    |    └── http     
    |        └── middleware
    |        └── rest 
    └── infra
        └── db
</pre>

## golang with lamda reccomend architecture 

<pre>
.
├── go.mod
├── go.sum
├── serverless.yml
|
├── config
└── lib
└── app
    └── domain
    |    └── model
    |    └── repository
    └── handler
    |    └── cmd
    |    └── parametor
    └── usecase  
    └── infra
        └── mysql
        └── s3
        └── ex...
</pre>


### model
- データのモデルを定義

### repository
- Usecase層で実装している処理のインターフェースを定義

### cmd
- ラムダ関数を定義
 
### parametor
- DTOモデル定義
- オブジェクトの変換処理

### infra
- 外部API、ライブラリとのクライアントオブジェクトを定義
- CRUD操作等

### usecase
- ビジネスロジックを記述（技術的な要素は省く）
    - インプットデータ
    - 入力チェック
    - アウトプットデータの作成　など

# Reference architecture
## Gorm
- https://gorm.io/ja_JP/docs/index.html
- https://github.com/volatiletech/sqlboiler

## DI（Dependency Injection）
- https://github.com/google/wire

