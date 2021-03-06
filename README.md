[![Jump to Wiki](https://img.shields.io/badge/TeamDoc-GitHubWiki-yellow)](https://github.com/jphacks/D_2001/wiki)


[![CircleCI](https://circleci.com/gh/jphacks/D_2001.svg?style=shield)](https://app.circleci.com/pipelines/github/jphacks/D_2001)

# name_it

[![name_it](doc/name_it.png)](https://youtu.be/6HeX8ccLHQo)

## 製品概要
　
### ネーミング x Tech

開発中になんとなく変数名やメソッド名を決めてもモヤモヤするときありませんか？

「書いてみたけどこれでちゃんと伝わるかな〜」

「もっと良い名前がある気がする...！」

そんな時はこの"**name_it**"でみんなに聞いてみましょう！
このサイトでは自分が悩んでいる変数名やメソッド名を投稿し、
みんながアンケートに投票や更なる選択肢の追加などを行って
よりよいネーミングを共有していくエンジニア支援サイトです。

### 背景(製品開発のきっかけ、課題等）

私たちCammelは2年前に「アジャイルを学び、実践する」という理念の元、大学の同期で立ち上げた開発チームです。
チーム開発の中で私たちが頭を抱えている課題は「**メンバーに伝わるコード**」を書くことの難しさでした。
最近の開発では**命名規則**を決めたり、**リファクタリング**をチームで行うことで、この課題に取り組んできました。

「[リーダブルコードーより良いコードを書くためのシンプルで実践的なテクニック](https://www.oreilly.co.jp/books/9784873115658/)」にはネーミングについて以下のように書かれています。

> 「**名前に情報を詰め込む**」　つまり、名前を見ただけで情報を読み取れるようにする

> 最善の名前とは、誤解されない名前である

このように**情報の詰め込み方**や**誤解のされない**ネーミングのためには、**開発者としての経験や知見**がとても重要であると私たちは考えました。

本プロダクト**name_it**では、開発者の知見を元により良いネーミングへの知見を得ることができます。

### 製品説明（具体的な製品の説明）

ネーミングに関する悩みを持つ人が悩みを投稿し、
回答者が投稿に対する回答としてネーミングの選択肢に投票や選択肢追加をします。

### 特長
#### 1. 特長1

学習された翻訳エンジンによってネーミングを生成する[codic: プログラマーのためのネーミング辞書](https://codic.jp/)とは異なり、実際のエンジニアの経験や知見を元にした**生の票**によって**より伝わりやすいネーミング**のための知見を得ることができます。

暫定的に名前を決めるためであれば、ユーザは**codic**を利用すると思います。
しかし、私たちの**name_it**ではリファクタリングやチームでのコード共有のタイミングに焦点を置きました。

**name_it**を使うことでより良いネーミングへの知見を共有してもらいたいと考えています。

#### 2. 特長2
GitHub連携によりユーザ登録ができます。

より経験のあるエンジニアの票に重み付けがされるようになっています。

#### 3. 特長3
markdown形式で投稿に対する説明を記述できます。
これによって回答者は説明文だけでなく実際のコード(markdownによるコード埋め込み)といった背景情報を元に投票や選択肢追加ができます。

また、コメント機能を使ってより良いネーミングについてのディスカッションを行ったり、
投稿をお気に入り登録して投票結果を追うことができます。

### 解決出来ること
開発者の経験を元にした投票結果によって、リファクタリングやチームとのコード共有の際に必要な知見を得て、ネーミングに対する悩みを解消することができます。

### 今後の展望
#### ベストアンサー率の追加
回答者のベストアンサー率を追加することでより信頼のできる回答者がわかるようにしたいと考えています。

#### 投稿のラベリング
投稿へのラベリング機能を追加することで似たような悩みを持つ人の投稿を検索できるようになります。

#### ランクのアップデート
[GitHub Readme Stats](https://github.com/anuraghazra/github-readme-stats)による、より多くのパラメータを用いたランクを採用したいと考えています。

#### より良いネーミングの知見が集まる場所へ
今後ユーザや投稿が増えていくことによって、name_itにより良いネーミングの知見が集まる場所になると考えています。

### 注力したこと（こだわり等）
* より開発経験のある人の票に価値があるようにGitHub Readme Statsの統計データを使用しました
* 想定するユーザ層(実際に私たちと同じように一度決まったネーミングに対して時間をかけて再考する人)の調査のためにTwitterのPoll機能で投票を取りました
* 基本的な機能が備わった段階でフィードバックをいただくためにTwitterにてリリース情報を投稿しました([v0.1.2リリース時](https://github.com/jphacks/D_2001/releases/tag/v0.1.2))
* オリジナルアイコンを作成しました
* 毎日DailyScrumや振り返りなど可能な限りアジャイルチックな開発を目指しました(詳しくは[Wiki](https://github.com/jphacks/D_2001/wiki)をご参照ください)
* 1Week=>1Day=>1Hourのフラクタルスプリントを採用して開発を進めました


<img width="500" src="https://user-images.githubusercontent.com/40158101/98358505-2982eb00-206a-11eb-9510-9427e248ec8b.png">

<img width="500" src="https://user-images.githubusercontent.com/40158101/98358461-15d78480-206a-11eb-8cb5-2266c652789e.png">

## 開発技術
### 活用した技術

#### フレームワーク・ライブラリ・モジュール
* Vue.js
  - vue-markdown
  - bootstrap-vue
* Firebase
  - Firebase Hosting
  - Cloud Firestore
* CircleCI

#### デバイス
* PC
* スマートフォン

### 独自技術
#### ハッカソンで開発した独自機能・技術
* ユーザ情報と投稿情報を相互に結び付けるデータベース構造
* GitHub情報を利用した投票数設定
