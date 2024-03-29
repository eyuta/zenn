# DBRE 輪読会 vol.02

これから DBRE 本 2 章の輪読会を始めます。

## 前回のおさらい

まずは軽く前回のおさらいから。
前回は、

- 学ぶことを楽しみ自己鍛錬を続けよう
- エンジニアとしてオペレーションのプロフェッショナルになろう
- チームの壁をなくして改善を進めよう

といったことに触れました。
その中で、DBRE の仕事の一つとして、SLO、サービスレベルオブジェクティブ、日本語でいうサービスレベル目標の違反の防止がありました。
今回は、その SLO について詳しく見ていきます。

## サービスレベルマネジメント

SLO を定義し、運用することを、本書ではサービスレベルマネジメントと呼んでいます。
サービスレベルマネジメントについて、本書では

"サービスがあるべき運用レベルを見定めること。これがサービスの設計、ビルド、デプロイにあたって最初にすべきことです。"

と書かれています。

## この章で学ぶこと

このサービスレベルマネジメントについて、どんな項目をどのように定義すればよいのか、定義した項目について、運用レベルを見対しているかどうかを、どう測定・監視するのか、について、詳しく見ていきます。

## 目次

目次はこの通りです。
最初に SLO についておさらいした後、SLO の各指標とその定義、監視方法について学びます。

## 目次

## 1. SLO とは

SLO とは、システムを設計・運用する際に、遵守すべき数値目標をまとめたものになります。

SLO が無いと、仮にシステムがダウンした時、そのダウンタイムが運用上許容されるのか、それとも重大な問題として直ちに対処しなければならないのか、判断することができません。
SLO があれば、そのダウンタイムが SLO を満たしているのであれば許容でき、SLO に違反しているのであれば何らかの対処が必要、といった判断をくだすことができます。

他にも、システムが安定に稼働しているか、アーキテクチャの変更が必要かどうか、システムが SLO を満たしているかどうかで判断することができます。

一方 SLA、サービスレベルアグリーメント、サービスレベル契約には、 SLO が特定のレベルを満たすことを約束する契約が規定されています。この規定に違反した場合、何らかのペナルティが課せられます。

## 1. SLO とは

例として、こちらは Amazon ec2 における SLA の一部になります。
Amazon EC2 はサービスレベル契約として月間可用性 99.99%を保証しているので、こちらに違反した場合、利用者はこの図の金額を受け取ることができます。

ただ、SLA はあくまでも SLO に基づく指標ですので、本書では触れません。

## 1. SLO とは

しかし、ここに示すように SLO を定める、つまりサービスレベルマネジメントを行うのは非常に難しいです。

98%のユーザーは 99.99%の可用性を提供できるが 2%のユーザーには 30%の可用性しか提供できない場合はどうするのか、
DB において、ユーザーがその損失に気づかない場合はどうするのか。
エラー発生率は全体の時間で平均して算出するのか、閾値を超えた数をカウントするのか。
等々、様々なケースが存在するためです。

## 1. SLO とは

SLO を定義する際にもっとも重要なことは、その指標がユーザー体験、ひいてはユーザー満足度を反映しているかどうかです。

## 目次

次に、SLO の指標と定義方法についてみていきます。

## 2. SLO の指標と定義

SLO の内容はあくまでサービスによって変わります。
しかし、先程も触れたようにあくまでもユーザーを中心に考えていきます。
次から、代表的な指標であるレイテンシ、可用性、スループット、耐久性、費用対効果の定義方法をみていきます。

### 2.1. レイテンシ

レイテンシは、レスポンスタイム、RTT とも呼ばれる指標です。
1 リクエストに対するレスポンスにかかる時間を表します。
このように、レイテンシの増加は、ビジネスに多大な影響を与えます。

### 2.1. レイテンシ

レイテンシの表記例についてみていきます。
ネットワークの通信速度は 0 にはならないこと、
レイテンシの実測値のうち、極端に高いものはノイズになるため取り除くと、

"リクエストの 99%において、レイテンシは 25 ミリ秒から 100 ミリ秒の間でなければならない"

といった形で表します。

### 2.2. 可用性

次に可用性です。
システムが利用可能である状態を、パーセンテージで示したものです。
9 を用いて 99.9%の可用性を提供する、といった言い方をします。

本書では、レイテンシと合わせて評価するべき、とあります。
もし指標がレイテンシだけの場合、レイテンシが既定値より高いと、クライアントはサービスが利用可能ではない、と判断する可能性があります。たとえサービスがダウンしておらず、リクエストに時間がかかっていた場合でも、です。

可用性を合わせて測定した場合、それらのリクエストについて、サービスが利用可能だったかどうかまでを知ることができます。

### 2.2. 可用性

SLO の表記はこのような形になります。
可用性のパーセンテージを定めることで、一定時間のダウンタイムを許容することができるようになります。

### 2.3. スループット

スループットは、一定時間において正常に処理されたリクエストの割合のことです。
サービスが対応可能な最大値を設定します。

割合、とありますが、個人的には数の方がしっくりきました。

例えば、システムが 1 秒間に 50 件のレスポンスを返せる場合は 50 件/秒のように表します。

### 2.4. 耐久性

ストレージに対して一定の成功率で書き込みができるかどうかを表します。

Amazon S3 の 99.999999999% 、通称イレブンナインが有名です。

### 2.5. 費用対効果

何かにかけた費用に対して、1 ページビューや購入 1 回など、特定のユーザーの行動にどの程度効果が出たかを、費用対効果で表します。

何のために費用をかけたのか、認識することが重要です。
EC サイトであれば、トランザクション数をどれくらい上げるために、いくらの費用をかけたのか、というのを認識する必要があります。

### 2.6. サービスを運用するために求められること

サービスを運用していくにあたっては、次の運用アクションが求められます。

新規サービスの場合、運用の指針となる SLO を定義し、その SLO として参照されるメトリクスに対して、目標及び実測値を適切に評価できる監視システムを設定します。

### 2.6. サービスを運用するために求めら

既存サービスの場合、サービスの過去と現在の状態を踏まえ、今までに達成した SLO と違反した SLO に対して、定期的なレビューを行う必要があります。

新規サービス、既存サービス関わらず、SLO を設定した後に、サービスレベルに影響をあたえうる不安要素を整理し、特定の不具合に対する回避策や修正度合いを検討する

### 2.7. SLO を定義する際に注意すること

新しいサービスを開始するにあたり、SLO を定義する際には以下の点に注意すべきです。

ユーザー中心
ユーザーにとって最も失われてはならないものから、SLO を組み立てます

あれもこれもと欲張らない
注目すべき指標のリストは、ダッシュボード 1 ページに収まる簡潔なものとします

SLO は定期的に見直すようにします。
ビジネスの段階によって、SLO に求められる内容が変わるためです。

## 目次

次に SLO に基づいた監視とレポート方法をみていきます。

## 3. SLO に基づいた監視とレポート

SLO の各指標を監視する上で重要なのは SLO を遵守することではなく、達成を妨げる潜在的なリスクを洗い出し、その対策をすることです。

SLO 違反のアラートを受けてから行動するのではなく、アラートを受ける前から不測の事態に対して SLO を遵守するための対応を取るようにします。

そのために、収集と分析の自動化、問題発生時のアラートの対応とその後のレポート、分析結果の視覚化の 3 つは、監視する値を決定する時点で考えておきたいです。
これらについては次章以降で詳しく触れます。

## 3.1. 可用性の監視

可用性の監視について、RUM（Real User Monitoring）と定点モニタリング(あるいは合成モニタリング、synthetic monitoring)を活用します。
Real User Monitoring はユーザーからのリクエストに対するエラー発生率を監視します。
理想は、累積したデータから近い将来のエラー発生率を予測し、週あたりのダウンタイムを超過する結果にならないか（SLO 違反とならないか）を判断できるようになることです。
ただし、サービスの状態はリリースによって更新されていくものなので、なかなか難しいものではあります。

## 3.1. 可用性の監視

監視に加えて、故意に作成したデータセットを用いたテストを走らせることも異常検知に役立ちます。これは定点モニタリングとも呼ばれます。
定点モニタリングがその効果を発揮するのは、カバレッジ計測をする場合です。ユーザーによって、サービスにアクセスする時間も地域もバラバラです。パフォーマンス測定用にチューニングされたクエリとカバレッジによってすべてのリージョンの時間を計測することで、特定の地域からのアクセスが不安定だったり遅かったりするのかを突き止め、対応できるようになります。

## 3.2. レイテンシの監視

次にレイテンシの監視です。
HTTP のリクエストログを、時系列のデータとして保存しておくことで、すべてのログをレイテンシの値でソートできます。
その上で、上位 1% のデータは分析から除外し、各 1 秒ごとの時間枠において、データの 99%が 100 ミリ秒を超えていた場合、SLO 違反としてダウンタイムを計上します。

## 3.3. スループットの監視

スループットの監視は、秒単位でトランザクション数を記録する形になります。

また、スループットは、測定、収集、そして可用性とレイテンシの SLO と絡めたレビューになるそうですが、こちら詳細については、次章以降で触れるようです。

## 3.4. 費用対効果の監視

費用対効果の監視は、定量化が難しいため、困難です。
クラウド環境の場合は、請求書からそれぞれどのくらいのコストが発生しているのか読み解きます。
また、人件費も考慮に入れる必要があります。

これらの作業の自動化は難しいです。
ただし、サービスを運用していくためにどれくらいの費用が必要なのかを把握することは、とても価値のあることです。

サービスが生み出した価値と、それにかかる費用をエンジニアが理解することで、技術的な観点から無駄を省き、燃費のよいアーキテクチャを設計する動機が生まれ、結果的に効率のよいコスト削減ができるようになるでしょう。

## 4. まとめ

最後に、本文の内容を引用します。

SLO を定義管理することは、インフラストラクチャを設計し運用する上での要石です。

サービス対するすべての施策は、SLO を遵守するための手段に過ぎません。

SLO が日々の活動全ての基礎なのです。
