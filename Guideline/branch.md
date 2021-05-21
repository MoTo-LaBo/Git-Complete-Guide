# branch (ブランチ)とは？
- 複数人で開発する場合は必至つの作業になる
- branch 並行して複数機能を開発する為にある
- merge  他の人が開発したものを自分の所に取り込む

>※ 特にこの時に事故が起こりやすい！人の変更を取り込んで今自分の作業環境が分からなくなってしまう事が多々ある。
## branchとは？
#### 並行して複数機能を開発する為にある機能
-  branch master をメインとして、分岐し開発していく為のモノ
- 他のチームメンバーの影響を受けないで自分の開発ができる

A　branch →　ヘッダーを修正

B　branch →　レコメンドを追加

A　＋　B　＝　master branch (deforuto の branch) に　merge （統合）させる
## branchの仕組み
>branch の仕組みを知るうえで Git の仕組みを知ることは非常に大切になってくる
#### 1. ワークツリー　 [fileを変更する作業場所]
>自分がコードを記述して作業している場所事を指す
- コードを記述している場所　＝　　ワーク　
- ディレクトリやフォルダー　　＝　　ツリー
#### 2. ステージングエリア　[コミットする変更を準備する]
>複数fileを変更したときに、コミットするfileを選択する為にあるエリア
#### 3. ローカルリポジトリ　[スナップショットを記録　コミット]
>fileやディレクトリを状態、変更履歴を記録する自身のPCの場所

- コミットはスナップショット。それが時系列順にい連なる
   - commit１ スナップショット１
   - commit２  スナップショット１
   - commit３ スナップショット１
   - commit3 に　master branch と　feature branch

## branch はコミットfileを指し示した　**【symbolic link】 symlink**
>シンボリックリンクとは、オペレーティングシステム（OS）のファイルシステムの機能の一つで、特定のファイルやディレクトリを指し示す別のファイルを作成し、それを通じて本体を参照できるようにする仕組み。
## HEAD
>今自分が作業しているbranchを指示しているpointer（作業している場所）
#### 例）Ａ
- master branch　**↓**　(HEAD)　

コミット　３　変更がありcommit　　　→　　　コミット４　master(HEAD)

- feature branch　**↑**
#### 例）Ｂ コミット３でbugがあり修正する事になった
- feature branch の方にブランチを切り替える　(HEAD)

コミット　３　　　　→　　　コミット４　master
#### ↑
- feature branch(HEAD) →　コミット４´feature branch(HEAD)

#### 例）Ｃ コミット４´で追加修正でcommit
- feature branch の方にブランチを切り替える　(HEAD)

コミット　３　　　　→　　　コミット４　master
#### ↑
- f b(HEAD) →　コミット４´f b(HEAD)　→　コミット５´　feature branch(HEAD)

#### 上記で分かるように並行して別の開発をする事ができる！
#### **branch と　HEAD の中身　ブランチはコミットIDを記録したポインタ**

- commit 4  master

**ハッシュID**　

「af5626b4a114abcb82d63db7c8082c3c4756e51b」という40文字の英数字

- commit 5' feature (HEAD)　[ HEAD fileの中身 　ref:feature レフ　参照]

**ハッシュID**　

「5626b4a114abcb82d63db7c8082c3c4756e51b」という40文字の英数字

- .git/HEAD
- .git/refs/　
- という .git/ の下の directory にデータが保存されている
## branch のまとめ
- 分岐する事で複数の機能を同時並行で開発する為の仕組み
- ブランチとはコミットを指すポインタ
####  スナップショットを記録しているのと相まって　↓
- ブランチの作成や切り替え、マージが他のバージョン管理ツールより高速
- Gitは大規模開発において最も使われるツールとなり普及


#### branch 新規追加
- $ `git branch ブランチ名`
- $ `git branch feature`

>※ branch の切り替えまでは行わない

- $ `git branch`　　　　　　何のブランチがあるか？表示・確認
- $ `git branch -a`　　　　-a は（all）remoteリポジトリの確認も含めて確認

>※ 今いる場所は、基本は緑色表示と＊(アスタリスク)
#### それぞれのbranchがどのcommitを指しているか？確認
- $ `git log --oneline --decorate`

>例）83bdcae (HEAD -> master, origin/master, feature) Update home.html
#### branchの切り替え
HEADの切り替え　＝　ポインタ　＝　自分の場所の作業の移動
- $ `git checkout 既存のブランチ名`
- $ `git checkout feature`

#### branch を新規作成して切り替えもする
- $ `git checkout -b 新ブランチ名`　　HEADがfeatureに移動

## branch名の変更と削除
##### 変更
- $ `git branch -m ブランチ名`
- $ `git branch -m new_branch`

>※　-m は move の略
##### 削除
- $ `git branch -d ブランチ名`
- $ `git branch -d feature`
- $ `git branch -D ブランチ名`　　　強制削除 ※ masterにマージされていなくても削除される

>※　この小文字の　-d （delete） の略。このコマンドは安全なコマンドと言われている

>master にマージされていない変更が残っている場合はそのブランチは削除されない。警告文を出してくれる。

**master branch へ merge したブランチは必ず削除する**
## branch を利用した開発
- master branch →　リリース用　branch
>※ 開発は topic branch を作成して進めるのが基本

- master branch を常に最新の状態に保たれる
- 今のリリースがどういうものか確認もできる
- リリースした後にバグがあっても、ひとつ前の master branch ver　をもう一回修正してリリースすれば、バグがない最新の状態を出せる
#### 「 **master branch はあくまでもリリース用としての使用が鉄則・基本の型**」
- master →　topic1 →　masterへmerge →　topic2 →　masterへmerge
- 上記の繰り返しで、開発したいものがあったときは最新の master branch から topic branch をきって開発していく。開発終了したら、master へ mergeする。

### **「 master branch を常に最新のverの状態にしておける 」**
## remote branch について
　リモートのブランチの状態へのポインタ

- ローカルリポジトリが古い状態にあり、remote リポジトリから最新の情報をfetchしてくる
- $ `git fetch`
- $ `git branch -a`
>※ 下記が表示される

>- master
>- remotes/origin/feature
>- remotes/origin/master

- origin/ ○○ブランチ名
>※ fetch してきた場合は上記の形で保存される
