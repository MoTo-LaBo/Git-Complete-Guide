# GitHub Flow
GitHub社のワークフロー
## 開発
1. master
2. branch
3. pull request
4. master へ merge　　1.へ戻る（merge した最新verの master へ）
## リリース
1. master
2. branch
3. commit
4. push
5. pull request
6. master へ merge
7. master branch をデプロイ　本番サーバーへ
#### **master branch は常に deploy できる状態を保つ**
>デプロイ（英: deploy）とは、「配置する」「配備する」「展開する」といった意味の英語の動詞です。 日本語の中では、ソフトウェア開発の工程のうち、開発した機能やサービスを利用できる状態にする作業を指す語として用いられています。
#### **新開発は master branchから新しいbranchを作成してスタート**
- master とは別に開発をしながら、運用できる
#### **作成した新しい branch 上で作業して commit する**
- コンフリクトを防ぐため
#### **新しい branch は定期的に push する**
- GitHubにpushする事で、最新の状態をチームメンバーと共有・確認できる
#### **master に merge する為に pull request 使用**
- 直接 master に merge しない。　レビューをしたいから。バグやコードの質を担保できない
#### master branch に merge したら直ぐに deploy する
- その為にテストと deploy は自動化をしておく
## なぜこのようなワークフローに落とし込むのか？
- 開発フローをシンプルに保ちたい。誰でも簡単にチーム開発に参入できるし開発できる
- master branch に merge したら直ぐに deploy する事によりリリースとmaster branch の状況が一致するので状況が理解しやすい。
- リリースした後でも、バグは機能単位での修正をしているので直ぐに元の状態に戻せる
