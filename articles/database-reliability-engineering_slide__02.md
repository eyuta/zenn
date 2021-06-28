---
marp: true
title: "【2章】データベースリライアビリティエンジニアリング【スライド】"
emoji: "🐕"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["oreilly", "DBRE"]
published: false
headingDivider: 3
theme: gaia
paginate: true
---

# DBRE 輪読会 vol.02

<!-- _class: lead -->

2021/07/01

## サービスレベルマネジメント

<!-- _class: lead -->

> サービスがあるべき運用レベルを見定めること。
> これがサービスの設計、ビルド、デプロイにあたって最初にすべきことです。

## この章で学ぶこと

- サービスの運用レベルについて、何をどのように定義するか
- 定義した運用レベルを満たすかどうか、どう測定・監視するか

## インデックス

1. SLO の必要性
2. SLO の指標と定義
3. SLO に基づいた監視とレポート
4. まとめ

## 1. SLO の必要性

- SLA: サービスを設計し構成するにあたり、一通りの仕様を定める
- SLO: 設計及び運用に関して遵守すべき事柄をまとめたもの

## 1. SLO の必要性

サービスレベルマネジメントは理解が難しい。

- API がリクエストを正常に処理したパーセンテージを記載する場合
  - その情報取得元をどうするか。API 自身？ サーバー？ DB？
  - 正常な場合は 200 を返すが、異常な場合は?
- ユーザーの行う無効・不正なリクエストは、どう取り扱うべきか

## 1. SLO の必要性

サービスレベルマネジメントは理解が難しい。

- 98%のユーザーは 99.99%の可用性だが、2%には 30%しか提供できない場合は？
- DB において、
  - 1 日分のデータが消失したが、影響範囲が特定のテーブルだけ
  - ユーザーがその損失に気づかない場合
  - 実際に消失したわけではなく、データが見つからない場合でもデータ消失として扱うべきか

## 1. SLO の必要性

サービスレベルマネジメントは理解が難しい。

- こちらに責任がない場合
  - 特定のユーザーのお粗末な wifi 環境やネット事情、中継ルータの問題で可用性が 95%となった場合、責任の所在は？

## 1. SLO の必要性

重要なのは、

#### その指標がユーザー体験、ひいてはユーザー満足度を反映

しているかどうか

## 2. SLO の指標と定義

SLO はサービスが持つ特性によって変わる。
ただし、SLO の中心として考えるべきはあくまでもユーザー。

### 2.1. レイテンシ

別名:レスポンスタイム、RTT(ラウンドトリップタイム)

1 リクエストに対するレスポンスにかかる時間を表す。
エンドツーエンドで測定するのがもっとも望ましい。

以下に示すように、レイテンシが 100 ミリ秒を超えると、ビジネスに多くの影響を及ぼす。

- Amazon: サイト表示が 0.1 秒遅くなると、売り上げが 1%減少し、
  1 秒高速化すると 10%の売上が向上する
- Google: サイト表示が 0.5 秒遅くなると、検索数が 20%減少する

### 2.1. レイテンシ

- ネットワークの通信速度は 0 にはならない
- レイテンシの実測値の中には極端に低いもの、高いものがある
  そのため、これらの外れ値を取り除く必要がある

これにより SLO は、

#### リクエストの 99%において、レイテンシは 25 ミリ秒から 100 ミリ秒の間でなければならない

となる。

### 2.2. 可用性

システムが利用可能である状態を、パーセンテージで示したもの。

- 利用可能である状態を、**どの時間**に対して適用するかを定めてはいけない
- その時間枠のすべてのリクエストが測定の対象。

### 2.2. 可用性

指標として、以下がある。

- 平均故障間隔: (MTBF: Mean Time Between Failures)
  - ダウンタイムがどれくらいの長さで発生するか示す
- 平均修復時間: (MTTR: Mean Time To Recover)
  - ダウンタイムからどれくらい早く回復するかを示す

### 2.3. スループット

一定時間において正常に処理されたリクエストの割合のこと
サービスが対応可能な最大値を設定する

参考: [SLO の導入  |  Cloud アーキテクチャ センター  |  Google Cloud](https://cloud.google.com/architecture/adopting-slos?hl=ja#throughput_as_an_sli)

### 2.4. 耐久性

ストレージに対して一定の成功率で書き込みができるかどうか。

例:
[Amazon S3 の耐久性](https://aws.amazon.com/jp/s3/storage-classes/#Performance_across_the_S3_Storage_Classes)

### 2.5. 費用対効果

TODO: 費用対効果の意味がほしい
費用は、1 ページビューや 1 購読数、購入 1 件といった行動に対して効果として測定されるべき。

費用対効果の指標を定義するにあたって重要なのは、かかったコストを何に対しての効果と捉えるべきか。

- ex.
  - コンテンツプロバイダ: ページビュー
  - オンラインサービス: ユーザー数
  - EC サイト: トランザクション数

### 2.5. 費用対効果

サービスを運用するにあたり、次のアクションが求められる。

- 新しいサービスの場合
  - 新しいサービスを開始するにあたり、運用の指針となる SLO(以下 SLA)を定義する
  - 新しいサービスの SLA として参照されるメトリクスに対して、目標及び実測値を適切に評価できるような監視システムを設定する

### 2.5. 費用対効果

サービスを運用するにあたり、次のアクションが求められる。

- 既存サービスの場合
  - サービスの過去と現在の状態を踏まえ、今までに達成した SLA と違反した SLA に対して、定期的なレビューを行う

### 2.5. 費用対効果

サービスを運用するにあたり、次のアクションが求められる。

- SLO 遵守率
  - SLO で定義した指標について、達成できているものとできていないものを確認する
- サービスに付随する問題
  - サービスレベルに影響をあたる不安要素を整理し、特定の不具合に対する回避策や修正度合いを検討する

### 2.6. SLO を定義する際に注意すること

- あれもこれもと欲張らない
  - 注目すべき指標のリストは、ダッシュボード 1 ページに収まる
    簡潔なものとする
  - たくさんあると、大切な指標を見逃してしまう
- ユーザー中心
  - ユーザーにとって最も失われてはならないものから、
    SLO を組み立てる
- SLO は定期的に見直す
  - ビジネスの段階によって、SLO に求められる内容が変わる

## 3. SLO に基づいた監視とレポート

SLO の各指標を監視する上で重要なのは SLO を遵守することではなく、達成を妨げる潜在的なリスクを洗い出し、その対策をすること。

SLO 違反のアラートを受けてから行動するのではなく、アラートを受ける前から不測の事態に対して SLO を遵守するための対応を取る。

そのために、以下の 3 つは監視する値を決定する時点で考えておく。

- 収集と分析の自動化
- 問題発生時のアラートの対応とその後のレポート
- 分析結果の視覚化

## 3.1. 可用性の監視

可用性の SLO が[上記](#回復力のあるシステム-vs-高い可用性のシステム)の場合、

- RUM(Real User Monitoring)に着目する
  - ユーザーからのリクエストに対するエラー発生率
  - 累積したデータから近い将来のエラー発生率を予測する
  - 上記から週あたりのダウンタイムを超過しないか判断できるようにする
    - 累積されたデータから将来の数値を予測する方法は多くある
  - 潜在的な問題に対し、データドリブンな観点から目を光らせ、深刻な障害を未然に防ぐ

## 3.1. 可用性の監視

可用性の SLO が[上記](#回復力のあるシステム-vs-高い可用性のシステム)の場合、

- 定点モニタリング
  - 故意に作成したデータセットを用いたテストを走らせることも、異常検知に役立つ
  - カバレッジ計測にその効果を発揮する
    - チューニングされたクエリとカバレッジによって、異なる時間、地域の測定を行う

## 3.2. レイテンシの監視

レイテンシの SLO が[上記](#リクエストの-99においてレイテンシは-25-ミリ秒から-100-ミリ秒の間でなければならない)の場合、HTTP のリクエストログを、時系列のデータとして保存する
上位 1%のデータを分析から除外した上で、各 1 秒毎の時間枠において、データの 99%が 100 ミリ秒を超えていた場合、SLO 違反としてダウンタイムを計上すべき。

## 3.3. スループットの監視

スループットは、測定、収集、そして可用性とレイテンシの SLO と絡めたレビューが必要。
秒単位でトランザクション数を記録しておき、スループットがトランザクション数を超えているか確認する。
超えられない場合、低規定に実施する負荷テストにおいて、度のタイミングで出力が落ちたのかを把握すべき。

## 3.4. 費用対効果の監視

クラウド環境でサービスを運用している場合、ストレージ、CPU、メモリ等々でどれだけコストが発生しているのかを読み解く必要がある。
サービスを運営する人件費も考慮する。人件費についても定期的に見直しが必要。
これらの事務作業は自動化は難しいが、サービスを運用するために発生するコストを把握する上で、とても価値がある。

> サービスが生み出した価値と、それにかかる費用をエンジニアが理解することで、技術的な観点から無駄を省き、燃費の良いアーキテクチャを設計する動機が生まれ、結果的に効率の良いコスト削減ができるようになるでしょう。

## 5. まとめ

> SLO を定義管理することは、インフラストラクチャを設計し運用する上での要石です。
> サービス対するすべての施策は、SLO を遵守するための手段に過ぎません。
> SLO が日々の活動全ての基礎なのです。

## 参考

- [Maintain SLO 〜俺たちの SLO はこれからだ!〜 | メルカリエンジニアリング](https://engineering.mercari.com/blog/entry/maintain-slo/)
- [レイテンシとは：定義から計測サイトまで用語にまつわるトピックを解説](https://ec-orange.jp/ec-media/?p=24447)
- [Web の表示が〇秒遅くなると ×× まとめ。Web パフォーマンスの重要性を示すフレーズ集 - アイデアマンズブログ](https://blog.ideamans.com/2019/03/web-performance-phrases.html)
- [担当マイクロサービスの SLI/SLO を見直そうと思ったんだ - エムスリーテックブログ](https://www.m3tech.blog/entry/2021/02/01/113000)