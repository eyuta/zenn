---
title: "AWS 認定ソリューションアーキテクト－プロフェッショナル～試験特性から導き出した演習問題と詳細解説～ 読書メモ"
emoji: "💯"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["aws", "sap", "certification"]
published: true
---

[AWS 認定ソリューションアーキテクト－プロフェッショナル～試験特性から導き出した演習問題と詳細解説～](https://www.amazon.co.jp/dp/B08F9CQ6LT/ref=cm_sw_em_r_mt_dp_S04TBK0WJSEYK3CXGMQ3)の読書メモ

## 1. 試験の概要と特徴

### 認定によって検証される能力

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/110860/47642b6e-1ef1-016f-c426-638d2059f266.png)

> 業界で広く知られている認定によって、技術的スキルと専門知識を証明し、キャリアアップにつなげます。
>
> - AWS で、動的なスケーラビリティ、高可用性、耐障害性、信頼性を備えたアプリケーションを設計し、デプロイする
> - 提示された要件に基づくアプリケーションの設計とデプロイに適した AWS のサービスを選択する
> - AWS で複雑な多層アプリケーションを移行する
> - AWS でエンタープライズ規模のスケーラブルな運用を設計し、デプロイする
> - コストコントロール戦略を導入する

引用: [AWS 認定ソリューションアーキテクト – プロフェッショナル](https://aws.amazon.com/jp/certification/certified-solutions-architect-professional/)

### 試験内容

> ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/110860/1d9e143d-6514-1e8e-24e0-2626b776408f.png)

引用: [AWS 認定ソリューションアーキテクト－プロフェッショナル 試験ガイド](https://d1.awsstatic.com/ja_JP/training-and-certification/docs-sa-pro/AWS-Certified-Solutions-Architect-Professional_Exam-Guide.pdf)

#### 1. 組織の複雑さに対応する設計 (12.5%)

- クロスアカウントの認証およびアクセス戦略
- ネットワークの設計
- マルチアカウントの設計
- IAM, VPC, VPC Flow Logs, CloudTrail 等が該当

#### 2. 新しいソリューションの設計 (31%)

- 以下を満たすソリューションの設計および実装戦略を決定する
  - セキュリティの要件および制御
  - 信頼性に関する要件
  - 事業継続性を確保する
  - パフォーマンス目標を達成する
  - ビジネス要件を満たす

#### 3. 移行の計画 (15%)

- クラウドへの移行が可能な既存のワークロードおよびプロセスを選択
- 新規の移行先ソリューションに適した移行ツールやサービスを選択
- 既存のソリューションに適した新しいクラウドアーキテクチャ
- 既存のオンプレミスのワークロードをクラウドに移行するための戦略

以下のようなサービスが該当する

> ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/110860/6668a974-db14-5959-dcb6-e6fae4fd2ed6.png)

引用: AWS 認定ソリューションアーキテクト－プロフェッショナル～試験特性から導き出した演習問題と詳細解説～ (Kindle の位置 No.177)

#### 4. コスト管理 (12.5%)

- ソリューションにおいてコスト効率に優れた料金モデルを選択
- コストを最適化するための管理設計、導入
- 既存のソリューションでコストを削減できる可能性を特定
- Cost Explorer, Budgets が該当
- EC2 の On-Demand, Reserved, Spot の使い分け

#### 5. 既存のソリューションの継続的な改善 (29%)

- ソリューションアーキテクチャのトラブルシューティング
- 既存のソリューションに対して、以下の戦略を決定する
  - オペレーショナルエクセレンスの実現に向けての改善
  - 信頼性の改善
  - パフォーマンスの改善
  - セキュリティの改善
  - デプロイメントの改善

## 2. 各種サービスの概要

### 2.01. 全体像

> ![service list](https://miro.medium.com/max/1400/0*3QXuNLMfyvH1L_vA.png)

引用: [How to pass AWS Solutions Architect Professional Exam? | by Talha Ocakçı | Medium](https://medium.com/@talhaocakci/how-to-pass-aws-solutions-architect-professional-exam-87bebfdae86f)
※こちらは全部網羅しているわけでは無いので、あくまでイメージで。

公式は[こちら](https://aws.amazon.com/jp/aws-jp-introduction/aws-jp-webinar-service-cut/)

### 2.02. コンピュート

ユーザーが開発したアプリケーションを、動的なスケーラビリティ、高可用性、フォールトトレランスを兼ね備えたシステムとして実行するために提供されるコンピューティングサービス。

- [EC2 (Amazon Elastic Computed Cloud)](https://www.slideshare.net/AmazonWebServicesJapan/20190305-aws-black-belt-online-seminar-amazon-ec2)
  - IaaS
  - 仮想サーバー
- [ELB (Elastic Load Balancing)](https://www.slideshare.net/AmazonWebServicesJapan/20191029-aws-black-belt-online-seminar-elastic-load-balancing-elb)
  - 負荷分散サービス
  - EC2, Lambda, コンテナ等の負荷分散が可能
  - ALB, NLB, CLB の違いを把握する
- [Elastic Beanstalk](https://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-online-seminar-2017-aws-elastic-beanstalk)
  - PaaS
  - ベースは EC2
  - アプリデプロイの自動化サービス
  - Java, Node, .NET, Go 等々に対応
- [Lambda (AWS Lambda)](https://www.slideshare.net/AmazonWebServicesJapan/20190814-aws-black-belt-online-seminar-aws-serverless-application-model-165314501)
  - FaaS
  - サーバーレスアーキテクチャ型のアプリケーション実行基盤を提供
- [AWS Batch](https://www.slideshare.net/AmazonWebServicesJapan/20190911-aws-black-belt-online-seminar-aws-batch)
  - バッチ処理のためのマネージドサービス
  - 大規模計算におけるバッチ処理を行う (夜間バッチのような用途ではない)
  - シミュレーションなど、負荷の高い計算をスーパーコンピューターやクラスタで順次実行する
- [ECS (Amazon Elastic Container Service)](https://www.slideshare.net/AmazonWebServicesJapan/20190731-black-belt-online-seminar-amazon-ecs-deep-dive-162160987)
  - CaaS
  - コンテナ型のアプリケーション実行基盤
  - コンテナの起動、停止、アクセス制御等を一元的に管理するコンテナオーケストレーションサービス
  - EC2 と Fargate を使用可能
- [EKS (Amazon Elastic Kubernetes Service)](https://www.slideshare.net/AmazonWebServicesJapan/20190410-aws-black-belt-online-seminar-amazon-elastic-container-service-for-kubernetes-amazon-eks)
  - k8s を利用したコンテナオーケストレーションサービス
- [Fargate (AWS Fargate)](https://www.slideshare.net/AmazonWebServicesJapan/20190925-aws-black-belt-online-seminar-aws-fargate)
  - ECS, EKS で利用可能なコンテナ実行コンピューティングエンジン
  - EC2 と異なり、パッチ適用やホストに対するセキュリティ対策が不要
  - ただし、ssh 等によるログインができない

### 2.03. ネットワーキング

ユースケースに応じて、インターネットや通信キャリアが提供する閉域網(専用線)、そして対応する AWS のネットワーキング関連サービスを正しく選択する必要がある。

- [VPC (Amazon Virtual Private Cloud)](https://www.slideshare.net/AmazonWebServicesJapan/20201021-aws-black-belt-online-seminar-amazon-vpc)
  - AWS 上にユーザーが構築可能な仮想ネットワークと、関連機能の総称
  - AWS は、VPC の利用を前提に設計・構築を行うことが多い
- NAT Gateway
  - VPC の一機能
  - インターネットへの通信経路を持たない EC2 インスタンスであっても、NAT Gateway を経由するとネットワークへアクセス可能
- VPC Endpoint
  - VPC の一機能
  - 各サービスに VPC Endpoint を作成することで、インターネットを経由せずに当該サービスに接続可能
  - VPC Endpoint には 2 種類ある
    - ゲートウェイエンドポイント: S3, DynamoDB のみ対応
    - インターフェースエンドポイント: 後述
- PrivateLink
  - VPC の一機能
  - VPC Endpoint のうち、インターフェスエンドポイントを PrivateLink と呼ぶ
  - PrivateLink を作成すると、VPC 内に専用の ENI が作成され、プライベート IP アドレスが割り当てられる
  - これにより、PrivateLink を経由して(インターネットを経由せずに)当該サービスへアクセス可能
- VPC Peering
  - VPC の一機能
  - VPC Peering を使うと、VPC 間のルーティングが行われ、通信が可能になる
  - 異なる AWS アカウント、リージョン間でも通信可能
- [Route 53 (Amazon Route 53)](https://www.slideshare.net/AmazonWebServicesJapan/20191016-aws-black-belt-online-seminar-amazon-route-53-resolver)
  - マネージド型の DNS サービス
  - インターネットや VPC 内の名前解決が可能
  - ルーティングポリシーに基づくトラフィックのルーティング、フェイルオーバーも可能
- [Direct Connect (AWS Direct Connect)](https://www.slideshare.net/AmazonWebServicesJapan/20210209-aws-black-belt-online-seminar-aws-direct-connect)
  - 通信キャリアの閉域網を経由して、オンプレミス環境と VPC 間で通信を行う
  - インターネット経由の VPN 接続より、安定しており、かつセキュリティも担保されている
  - 高い可用性を求める場合は複数のキャリアの回線を利用する
  - ただし、Direct Connect は VPN 接続よりも高価なため、バックアップには VPN 接続を用いるケースもある
- [AWS Managed VPN](https://www.slideshare.net/AmazonWebServicesJapan/amazon-vpc-vpn)
  - 前述したように、VPC とオンプレミス間で比較的安価に暗号化接続を行う手段の 1 つ
  - VPC とオンプレミスを接続するには、以下が必要になる
    - オンプレミス側: VPN 接続が可能なネットワーク機器
    - VPC 側: 上記のネットワーク機器に対応した Customer Gateway (CGW)
    - VPC 側: AWS 側の VPN 側の機能を有効化するための Virtual Private Gateway (VGW)

### 2.04. ストレージ、配信

AWS が提供する様々なストレージサービスから、データの利用用途やライフサイクルに応じて、適切なサービスを組み合わせる必要がある。

- [S3 (Amazon Simple Storage Service)](https://www.slideshare.net/AmazonWebServicesJapan/20190220-aws-black-belt-online-seminar-amazon-s3-glacier)
  - 高可用性・高耐久性のストレージサービス
  - AWS の各サービスのバックアップにも、スナップショットといった形で保存されることがある
  - 以下のようなユースケースに応じた使い方を理解する
    - データのアクセス頻度や耐久性等に応じたストレージクラスの使い分け
    - アクセス制御方法
    - S3 を利用した Web サイトホスティング
    - 暗号化、バージョン管理、ライフサイクル管理、etc
- [EBS (Amazon Elastic Block Storage)](https://www.slideshare.net/AmazonWebServicesJapan/20190320-aws-black-belt-online-seminar-amazon-ebs/)
  - E2 と共に扱う、ブロックストレージ
  - EBS ボリュームは EC2 の OS によってマウントされる
  - ボリュームがアタッチされる EC2 に求められる IOPS 性能やスループット性能に応じて、最適なボリュームタイムを選択する
  - EC2 と EBS はネットワークで接続されている。
  - そのため、帯域が十分に確保されていない場合、想定されたパフォーマンスを発揮できない
  - 以下で対応可能
    - EC2 のスペックをあげる
    - EC2 のインスタンスタイプを**EBS 最適化**にする
- [EFS (Amazon Elastic File System)](https://www.slideshare.net/AmazonWebServicesJapan/2018070420190520-renewed-aws-black-belt-online-seminar-amazon-elastic-file-system-amazon-efs)
  - NFS (Network File System) ファイルシステムサービス
  - 複数の EF2 インスタンスから同じ EBS をマウント可能
  - 以下をサポートしていない点には注意が必要
    - Windows で使用される SMB (Server Message Block)
    - Windows を OS として利用する EV2 インスタンス
- Glacier (Amazon S3 Glacier)
  - S3 のストレージクラスの一種
  - 安価に長期保存が可能
  - 最小ストレージ保存期間は 90 日
  - ただし、安価な代わりにアーカイブしたデータの取り出しに数時間かかる
  - (迅速取り出し(Expedited)を利用すると、コストは掛かるものの、数分で取り出せる)
- Glacier Deep Archive
  - Glacier より一層コスト削減が可能
  - ただし、
    - 最小ストレージ保存期間は 180 日
    - データの取り出しには 12 時間かかる
- [Storage Gateway](https://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-online-seminar-2017-aws-storage-gateway)
  - 主にオンプレミス環境のデータを仮想アプライアンス経由で S3 にバックアップするためのサービス
  - オンプレミス環境のサーバー群は残しつつ、データのストレージへのバックアップ部分のみを AWS 側にオフロードする
  - 以下の 3 つのタイプがある
    - ファイルゲートウェイ
      - S3 オブジェクトをバックエンドとしたファイルストレージ
    - ボリュームゲートウェイ
      - S3 及び EBS snapshots をバックエンドとしたブロックストレージ
    - テープゲートウェイ
      - S3 と Glacier にデータを保管する仮想テープストレージと VTL 管理
- CloudFront
  - CDN (Content Delivery Network)サービス
  - ユーザーが Web を通じて配信したいコンテンツをを CloudFront の中にキャッシュとして保持する
  - 世界中にエッジロケーションが存在するため、ユーザーに対する応答時間を短くできる
  - 静的コンテンツをエッジロケーションから返送することで、オリジン側の負荷を低減できる

### 2.05. データベース

- [RDS (Amazon Relational Database Service)](https://www.slideshare.net/AmazonWebServicesJapan/20180425-aws-black-belt-online-seminar-amazon-relational-database-service-amazon-rds-96509889)
  - MySQL, PostgreSQL, Oracle, SQL Server 等をマネージドで提供するサービス
  - コンソールや CLI で簡単に冗長構成(Multi-AZ)の環境を構築できる
  - 以下の機能により、最短で 5 分前の状態に DB を復元するポイントインタイムの復元機能 (Point-in-Time Recovery)を提供する
    - デフォルトで日次のバックアップを取得する
    - 定期的にデータ断面のスナップショットを S3 に保存する
- [Aurora (Amazon Aurora)](https://www.slideshare.net/AmazonWebServicesJapan/20200929-aws-black-belt-online-seminar-amazon-aurora-mysql-compatible-edition)
  - RDB の一種
  - [MySQL](https://www.slideshare.net/AmazonWebServicesJapan/20190424-aws-black-belt-online-seminar-amazon-aurora-mysql)と[PostgreSQL](https://www.slideshare.net/AmazonWebServicesJapan/20190828-aws-black-belt-online-seminar-amazon-aurora-with-postgresql-compatibility-168930538)をクラウド環境に最適化させたサービス
  - [AWS によると、標準的な MySQL と比べて 5 倍、PostgreSQL と比べて 3 倍高速になる](https://aws.amazon.com/jp/rds/aurora/?aurora-whats-new.sort-by=item.additionalFields.postDateTime&aurora-whats-new.sort-order=desc)
  - プライマリインスタンスに障害が発生した場合、リードレプリカがプライマリに昇格する
- [DynamoDB (Amazon DynamoDB)](https://www.slideshare.net/AmazonWebServicesJapan/20170809-black-belt-dynamodb)
  - キーとバリューの組み合わせでデータが保存される、キーバリュー型の NoSQL データベースサービス
  - 保存されたデータは 3 つの AZ に複製されるため、高いスケーラビリティを確保できる
  - DynamoDB のスループットはテーブル単位で指定された RCU(Read Capacity Unit), WCU(Write Capacity Unit)によって定まる
  - RCU, WCU は、以下を考慮して計算する
    - テーブルに保存されるデータのサイズ
    - 強い一貫性が必要かどうか
    - 1 秒あたりに発生するべき Read や Write の数
- [ElastiCache (Amazon ElastiCache)](https://www.slideshare.net/AmazonWebServicesJapan/aws-black-belt-online-seminar-2017-amazon-elasticache-84060910)
  - マネージド型のインメモリデータストア
  - データストアのエンジンとして Redis, Memcached を選択可能
  - データがメモリの中に格納されているため、高速に返却できる
  - RDS への問い合わせが頻繁に発生するデータについて ElastiCache にキャッシュすることで、レスポンスタイムを短縮可能
  - また、セッション情報を保存するユースケースもある
    - セッション情報を ElastiCache に保存することで、アプリケーションをストートレスに保てる
- [Neptune (Amazon Neptune)](https://www.slideshare.net/AmazonWebServicesJapan/20200714-aws-black-belt-online-seminar-amazon-neptune)
  - グラフモデルを効率的に格納し、検索するためのグラフデータベースサービス
  - プロパティグラフと RDF をサポート
  - SNS, 路線図、WWW 等、いたるところで活用される
- [Redshift (Amazon Redshift)](https://www.slideshare.net/AmazonWebServicesJapan/20200318-aws-black-belt-online-seminar-amazon-redshift)
  - PostgreSQL に基づいた、データ分析に特化したデータウェアハウスサービス
  - データは列指向(カラムナ)型で格納されるため、特定の列に保存されたデータの集計を高速に行える
  - 数十程度のクライアントが業務分析を行うようなワークロードに最適化されている

### 2.06. アナリティクス

### 2.07. アプリケーション結合

### 2.08. AI サービス

### 2.09. セキュリティ、アイデンティティ、コンプライアンス

### 2.10. 管理ツール

### 2.11. コスト最適化

### 2.12. 移行

### 2.13. 開発者ツール

## 3. 試験で問われるシナリオの特性

### 3.01 「組織の複雑さに対応する設計」

### 3.02 「新しいソリューションの設計」

### 3.03 「移行の計画」

### 3.04 「コスト管理」

### 3.05 「既存のソリューションの継続的な改善」

## 4.「組織の複雑さに対応する設計」の問題例

## 5.「新しいソリューションの設計」の問題例

## 6.「移行の計画」の問題例

## 7.「コスト管理」の問題例

## 8.「既存のソリューションの継続的な改善」の問題例

## 9. 模擬試験
