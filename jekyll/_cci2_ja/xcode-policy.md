---
layout: classic-docs
title: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
short-title: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
categories:
  - platforms
description: Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて
order: 31
version:
  - Cloud
---

* 目次
{:toc}

## 概要
{:.no_toc}

ここでは、Xcode イメージのリリース、更新、サポート終了に関する CircleCI のポリシーについて説明します。 CircleCI では、ベータ イメージを含め、新しいイメージのリリースを切れ目なくスピーディかつ円滑に行うため、Xcode イメージについて明確なポリシーを定めています。

## Xcode イメージの維持およびサポート終了

CircleCI では、Xcode のメジャー バージョンを 4 つまで維持し、新しいバージョンについては複数のイメージを提供することを目標とします。

Xcode 12 が最新のリリース済みメジャー バージョンである執筆時点では、次のようになります。

| Xcode のバージョン | 対応                                                            |
| ------------ | ------------------------------------------------------------- |
| Xcode 12     | すべての major.minor バージョンについて最新のパッチ バージョンを維持します                  |
| Xcode 11     | すべての major.minor バージョンについて最新のパッチ バージョンを維持します                  |
| Xcode 10     | 今後の Xcode 12 リリースの発表に応じて、過去の Xcode 10 バージョンに対するサポートを段階的に終了します |
| Xcode 9      | Xcode 9 の最新の安定版リリースとなるイメージ 1 つのみを維持します                        |
| Xcode 8      | 完全に削除されました                                                    |
{: class="table table-striped"}

今後、Xcode 13 のベータ イメージがリリースされた場合の維持の例は次のようになります。

| Xcode のバージョン | 対応                                                                                       |
| ------------ | ---------------------------------------------------------------------------------------- |
| Xcode 13     | ベータ イメージ ポリシーに従いベータ イメージをリリースおよび更新します                                                    |
| Xcode 12     | すべての `major.minor` バージョンについて最新のパッチ バージョンを維持します                                           |
| Xcode 11     | ベータ期間中はすべての `major.minor` バージョンについて最新のパッチ バージョンを維持し、Xcode 13 のリリース サイクル開始後はサポートを段階的に終了します |
| Xcode 10     | Xcode 13 の GM 版がリリースされ次第、最終リリースを除くすべてのイメージをサポート終了対象とします                                  |
| Xcode 9      | Xcode 13 の GM 版がリリースされ次第、サポート終了対象とし、削除します                                                |
{: class="table table-striped"}

特定のイメージがサポート終了対象および削除対象となった場合、[CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)でお知らせするとともに、最近実行されたジョブでいずれかの廃止対象イメージをリクエストした開発者の方々にメールで通知します。 CircleCI では、廃止の 4 週間前に通知することを目標とします。

イメージに対するリクエストが別の major.minor バージョンに自動でリダイレクトされることはありません。そのため、廃止予定のイメージを指定している設定ファイルは手動で更新する必要があります。イメージの削除までに設定ファイルが更新されなかった場合、ジョブでリクエストされるイメージのいずれかが削除された時点で、ジョブは失敗するようになります。

## Xcode のパッチ

CircleCI では、サポート対象の各マイナー バージョン単位で最新のパッチ バージョンを維持します。 新しいパッチ バージョンがリリースされた場合、過去のパッチ バージョンのサポートを終了し、すべてのリクエストを新しいパッチにリダイレクトします。

通常、パッチには後方互換性が備わっているため、このリダイレクトは新パッチのリリースから 24 時間以内に開始されます。 深刻な問題が確認された場合には、ロールバックを行い、暫定的にどちらのバージョンも利用可能にします。

**例:**

Xcode `12.0.1` がリリースされた時点で、過去のパッチ バージョンである `12.0.0` を削除し、`12.0.0` に対するすべてのリクエストを `12.0.1` にリダイレクトします。

## ベータ イメージのサポート

Xcode の次回安定版リリースよりも前に開発者の方々がアプリのテストを行えるように、可能な限り早期に macOS Executor で Xcode のベータ バージョンを公開できるよう尽力します。

ベータ イメージについては、安定版イメージ (更新が停止されたもの) と異なり、GM (安定版) イメージが公開され更新が停止するまでは、新規リリースのたびに既存のイメージが上書きされます。 ベータ版の Xcode バージョンを含むイメージをリクエストする場合は、Apple から Xcode の新規ベータ版が公開され次第、最小限の通知とともにそのイメージに変更が加えられることをご了承ください。 こうした変更には Xcode および関連ツールに対する、抜本的で CircleCI としては不可抗な変更も含まれます。

ベータ版イメージに関する CircleCI のお客様サポート ポリシーについては、[サポート センターに関するこちらの記事](https://support.circleci.com/hc/ja-jp/articles/360046930351-What-is-CircleCI-s-Xcode-Beta-Image-Support-Policy-)をご覧ください。

## Xcode イメージのリリース

CircleCI では Apple の Xcode のリリース状況を注意深く追跡し、常に可能な限り迅速に新しいイメージをリリースするよう努めます。作業にかかる時間が Xcode と macOS に加えられた変更の量に大きく依存するため、リリースについて SLA として所要時間を公式に定めることはいたしません。

新しいイメージがリリースされた際は常に、[CircleCI の Discuss サイト](https://discuss.circleci.com/c/announcements/39)でリリース ノートを添えてお知らせします。また、[こちらの Xcode バージョンの表(英語)](https://circleci.com/docs/2.0/testing-ios/#supported-xcode-versions)に追記します。

## macOS のバージョン

各 Xcode イメージは、macOS のクリーン インストールを基盤としています。 CircleCI では、macOS バージョンの更新を Xcode の必要最小バージョンが上がったときにのみ行い、できる限りバージョンを一定に保つことを目指します。 Xcode の必要最小バージョンが上がった場合は、macOS のバージョンを最新の安定版バージョンに更新します。

macOS の新しいメジャー バージョン (`10.15` や `11.0` など) がリリースされた場合、重大なバグや問題が発生した際に解決できるように、通常は Xcode のマイナー バージョンが 2 つ以上リリースされた後からそのバージョンの使用を開始します。 このリリースのタイミングは Apple のリリース サイクル次第ですが、必ず事前に [CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)で告知します。

## 例外

CircleCI は、どのような場合でも、状況に応じて本記事の説明内容とは異なる措置を講じる権利を保有しています。 本ポリシーの例外を実施する必要がある場合、可能な限り十分な告知を行い、最善の透明性を維持するよう努めます。 こうした場合、[CircleCI Discuss フォーラム](https://discuss.circleci.com/c/announcements/39)に告知を掲載するとともに、可能であればメールなどでの通知も行います。