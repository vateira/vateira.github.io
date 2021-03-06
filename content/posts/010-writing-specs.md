---
title: "アジャイルな開発でも仕様をドキュメント化することについて"
date: 2021-05-06T22:24:39+09:00
tags: ["コラム", "プロマネ"]
---

アジャイルな開発ではドキュメントレスが取り上げられ、テストファーストが重要視されることから、仕様をドキュメントにまとめるということについてこれまでの体感では賛否両論色々あるように思う。
ここ三年ほど関わっている web サービスのプロジェクトでは、特にサーバーサイドに関しては仕様記述を割合しっかりと行っている。

<!--more-->

このプロジェクトでは、最初はクライアントサイドとサーバサイドの両方において VDM++を使い仕様ドキュメントを作成していた。
といっても主にクライアントサイドは陰関数定義などが主体であり、trace などを使った仕様の検証はあまりしなかったがメンバーが共通の書き方で仕様を作成できてツールによって文法チェックができるという点で非常に良かったと思う。

ただし、いくら軽量形式手法とはいってもそれなりに作成に工数がかかることは事実で、ここ二年弱はクライアントサイドは yaml 形式で画面の構成とコントロールに対するイベントを決まった構造で記述し自前のツールで検証して markdown のドキュメンに変換するような DSL へと変わっていった。サーバサイドについても lalrpop を使って json と VDM++が合わさったようなシンタックスの DSL をチームで作り、それを用いるようになっている。
オレオレ仕様記述は結構色々なところで作られては結局一般的なツールに戻るという話をよく聞くが、現在のプロジェクトでは検証ツールとしての機能性よりも如何に簡単に必要最低限のことができるかに重きを置いているので、それなりに上手くいっているように思う。

ただし、やはり大切なのはチームとの相性だろう。  
現在のチームはもともとそういった技術に興味のあるメンバーで構成されているから回っているというのは事実で、エンジニアの関心ごとが別にあればよくある web サービスで導入することが費用対効果に合うかどうかは要検討だ。
例えばこのチームでは、仕様は json に変換されるのでそれを元にテストコードを生成するツールを実験的に作成してるメンバーもいたりするので、そういった場合は相性が良いだろう。
特にクライアントサイドについては非機能要件の改修や A/B テストなどの日々のマイナーアップデートなどもあるので、リソース的に厳しいことはよく感じている。

個人的には仕様記述により仕様ドキュメントが残っていると、PM としてはエンジニアに確認を取ったり実装を追ったりせずとも仕様が分かるので、PO からのユーザーストーリーをタスクに落とし込む際などに非常に助かっているし、開発メンバー等も slack で実装の議論をする際にドキュメント化された仕様をベースにやりとりをしているので、一般的な web サービスでもそういったコミュニケーションの助けとしても非常に有効かなと思う。
