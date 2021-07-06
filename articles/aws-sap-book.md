---
title: "AWS 認定ソリューションアーキテクト－プロフェッショナル～試験特性から導き出した演習問題と詳細解説～ 読書メモ"
emoji: "🌊"
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

### 2.04. ストレージ、配信

### 2.05. データベース

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
