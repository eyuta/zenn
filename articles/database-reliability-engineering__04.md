---
title: "【3章】データベースリライアビリティエンジニアリングの読書メモ"
emoji: "😺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["oreilly", "DBRE"]
published: false
---

[O'Reilly Japan - データベースリライアビリティエンジニアリング](https://www.oreilly.co.jp/books/9784873119403/) の 4 章の読書メモです。

## Table of Contents <!-- omit in toc -->

- [4. オペレーション](#4-オペレーション)
  - [4.1 現在の見える化の標準仕様](#41-現在の見える化の標準仕様)
    - [4.1.1 見える化を BI のように扱う](#411-見える化を-bi-のように扱う)
    - [4.1.2 仮想環境におけるクラスタの見える化](#412-仮想環境におけるクラスタの見える化)
    - [4.1.3 高分解能でのメトリクス収集](#413-高分解能でのメトリクス収集)
    - [4.1.4 アーキテクチャをシンプルに保つ](#414-アーキテクチャをシンプルに保つ)
  - [4.2 OpViz フレームワーク](#42-opviz-フレームワーク)
  - [4.3 データの入力](#43-データの入力)
    - [4.3.1 テレメトリ／メトリクス](#431-テレメトリメトリクス)
    - [4.3.2 イベント](#432-イベント)
    - [4.3.3 ログ](#433-ログ)
  - [4.4 データの出力](#44-データの出力)
  - [4.5 監視の第一歩](#45-監視の第一歩)
    - [4.5.1 データは安全か](#451-データは安全か)
    - [4.5.2 サービスは落ちていないか](#452-サービスは落ちていないか)
    - [4.5.3 顧客のサービス体験に痛みが伴っていないか](#453-顧客のサービス体験に痛みが伴っていないか)
  - [4.6 アプリケーションの計器](#46-アプリケーションの計器)
    - [4.6.1 分散トレーシング](#461-分散トレーシング)
    - [4.6.2 イベントとログ](#462-イベントとログ)
  - [4.7 サーバーやインスタンスの計器](#47-サーバーやインスタンスの計器)
    - [4.7.1 イベントとログ](#471-イベントとログ)
  - [4.8 データベースの計器](#48-データベースの計器)
  - [4.9 データベースの接続レイヤ](#49-データベースの接続レイヤ)
    - [4.9.1 利用率](#491-利用率)
    - [4.9.2 リソースの飽和点](#492-リソースの飽和点)
    - [4.9.3 エラー](#493-エラー)
  - [4.10 データベースの内部構造の見える化](#410-データベースの内部構造の見える化)
    - [4.10.1 スループットとレイテンシのメトリクスの見える化](#4101-スループットとレイテンシのメトリクスの見える化)
    - [4.10.2 コミット、再実行、ジャーナリングの見える化](#4102-コミット再実行ジャーナリングの見える化)
    - [4.10.3 レプリケーション状態の見える化](#4103-レプリケーション状態の見える化)
    - [4.10.4 メモリ構造の見える化](#4104-メモリ構造の見える化)
    - [4.10.5 ロックと並行性の見える化](#4105-ロックと並行性の見える化)
  - [4.11 データベース内オブジェクトの見える化](#411-データベース内オブジェクトの見える化)
    - [4.12 データベースクエリの見える化](#412-データベースクエリの見える化)
    - [4.13 データベースのアサートとイベントの見える化](#413-データベースのアサートとイベントの見える化)
    - [4.14 まとめ](#414-まとめ)

## 4. オペレーション

オペレーションの見える化(OpViz)は DBRE の要。
見える化によって日々変化する DB と付随するコンポーネントの状況を把握できる。

見える化のメリットは以下の通り。

- アラートの発生と収束
  - システムの壊れた or 壊れそうなタイミングを知ることで、SLO 違反を防ぐ
- パフォーマンス測定
  - 外れ値を含んだレイテンシを理解することで、現在のトレンドを把握できる
- キャパシティプラニング
  - リソースを有効に使用できていなければ、ここぞという場面でキャパシティ不足に陥る
- デバッグとポストモーテム
  - 問題の早期発見は早期解決につながる
  - 見える化によりシステム自体を改善し、回復力を高める
- ビジネス分析
  - ユーザーのシステム活用方法を知ることで、以下が分かる
    - 問題の与える影響を理解できる
    - システムのうち、価値を生み出している部分が分かる
    - その価値に対するコスト配分を考えるのに役立つ
- 原因と結果の相関分析
  - サービスに負荷がかかった際、インフラとアプリの両者がどのような動きをするのか分かる

この章では、OpViz の原則や分類、パターンを知る。

### 4.1 現在の見える化の標準仕様

見える化を進める理由は、

- この事象は SLO に対してどういった影響があるのか
- 障害はどのようにして、なぜ発生したのか

を知るため。

そのため、OpViz ツールは Ops チームだけではなく BI ツールとしても使う必要がある。
チームの垣根を超えて設計、構築、管理を行い、データを BI として活用できるようにする。

#### 4.1.1 見える化を BI のように扱う

究極の見える化とは、ビジネスがどのように動作し、アプリとインフラにより、ビジネスはどのような影響を受けるのかを、誰もが理解できる(=BI ツール)。

#### 4.1.2 仮想環境におけるクラスタの見える化

クラスタ構成の場合、個々のノードは常に動的。
そのため、メトリクスはホスト名や IP ではなく、マスター or スライブといったロール毎に保存されるべき。

#### 4.1.3 高分解能でのメトリクス収集

高分解能 == 1 秒以下のメトリクス収集感覚

頻繁に変化する CPU やデータベースの接続キューは、高分解能が必要。
一方で、ディスクの空き容量やヘルスチェックは 1 分以上のチェックで十分。

#### 4.1.4 アーキテクチャをシンプルに保つ

大事なことは、ノイズをゼロに抑えること。
多くのメトリクスを見るのではなく、アラートや人間の手が必要なレベルになる必要最小限のものに絞る。
本当に重要なメトリクスを見極め、取捨選択する文化を育てたい。

### 4.2 OpViz フレームワーク

OpViz は、以下のように大きな分散 I/O デバイスと捉えることができる。

- データ入力 → ルーティング → 構造化 → 出力

その出力結果により、以下が可能になる。

- システムをより理解するための監視
- 障害や障害の予兆の見える化
- SLO を満たしているかの判断

上記の I/O を詳しく見ていく。

### 4.3 データの入力

システムのモニタリング方法には、ブラックボックスモニタリングとホワイトボックスモニタリングがある。

1. ブラックボックスモニタリング

   - 以下からデータを収集する
     - サンプルとなるカナリアユーザー
     - インターネとからの入出力
   - 監視対象の期間やアイテムがそれほど多くない場合に有効な手段

2. ホワイトボックスモニタリング
   - 具体的に、どのアプリケーションのどの部分を監視するのかを決めておく必要がある
   - プッシュ型のアプローチを採用することで、

---

ブラックボックスモニタリング、ホワイトボックスモニタリングとは、以下のような違いがある。

- ブラックボックスモニタリング
  - システムの内部状態とメカニズムを確認しない
- ホワイトボックスモニタリング
  - システムの内部状態とメカニズムを確認し、それらの情報を収集する

参考: [DevOps 測定: モニタリングとオブザーバビリティ  |  Google Cloud](https://cloud.google.com/architecture/devops/devops-measurement-monitoring-and-observability?hl=ja)

---

モニタリングされた内容は、データ収集用のエージェントやクライアントによって収集される。
そして収集後、データタイプ毎に中央サーバーに格納される。
データ収集の方法には、サーバーが個々のクライアントにデータを取りにいくプル型と、個々のクライアントがサーバーにデータを送信するプッシュ型がある。

- プル型の特徴
  - 中央集権的な構成
  - コマンドを発行することで、各エージェントから必要な情報を収集可能
- プッシュ型の特徴
  - 分散構成
  - 監視対象をアーキテクチャ毎に分散できる (リソースの増減に対応しやすい)

#### 4.3.1 テレメトリ／メトリクス

#### 4.3.2 イベント

#### 4.3.3 ログ

### 4.4 データの出力

### 4.5 監視の第一歩

#### 4.5.1 データは安全か

#### 4.5.2 サービスは落ちていないか

#### 4.5.3 顧客のサービス体験に痛みが伴っていないか

### 4.6 アプリケーションの計器

#### 4.6.1 分散トレーシング

#### 4.6.2 イベントとログ

### 4.7 サーバーやインスタンスの計器

#### 4.7.1 イベントとログ

### 4.8 データベースの計器

### 4.9 データベースの接続レイヤ

#### 4.9.1 利用率

#### 4.9.2 リソースの飽和点

#### 4.9.3 エラー

### 4.10 データベースの内部構造の見える化

#### 4.10.1 スループットとレイテンシのメトリクスの見える化

#### 4.10.2 コミット、再実行、ジャーナリングの見える化

#### 4.10.3 レプリケーション状態の見える化

#### 4.10.4 メモリ構造の見える化

#### 4.10.5 ロックと並行性の見える化

### 4.11 データベース内オブジェクトの見える化

#### 4.12 データベースクエリの見える化

#### 4.13 データベースのアサートとイベントの見える化

#### 4.14 まとめ
