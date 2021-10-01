# GitHub & Git 完全ガイド

## New-Git_Guideline は submodule です
- submodule として Git Complete Guide に紐づいています
- Git Complete Guide clone 時は、New-Git_Guideline の file/direcotory 情報は clone されないので注意して下さい
- 下記のcommand で clone すれば、New Git Guideline のfile / direcotory 情報も一緒に clone されます
## Git Complete Gide cole時には submodule を初期化＆更新を実行
    git clone --recurse-submodules <url>
## submodule が更新された場合
- **親 project の submodule directory は常に最新の commit をさすわけではない**
- あくまでも別々の repositories なので submodule の中で個別に pull して情報を更新しないといけないが、下記の command をcurrent directory　で使用することで解決できる
### 全ての submodule でコマンドを実行 ※ current directory で実行
    git submodule forcach '<command>'
- git subumodule foreach `git pull origin main`コマンドを実行する事によって、各 subumodule で git pull origin main が実行される

## Gitの使用目的
### file verの管理システム
>一人でデータを管理する場合でも混乱する時がある。それが複数人で編集・共有する場合はもっと事故が起きやすい。それを未然に防ぐ為のシステム。間違って上書きや削除した場合でも修復できる。
- fileの最新の状態が分かる
- いつ・誰が・何を下か分かる
- 以前の状態に戻せる
- 間違って上書き前しようとした場合警告が出る（未然に事故を防ぐ事ができる）
### GitとGitHubとの歴史
>開発を迅速に行えるように開発されている
- スピード
- シンプル
- ブランチが並列で開発可能
- 大規模プロジェクトを効率的に取り扱える
### GitHubとは？
#### gitリポジトリーのホスティングシステム
>fileの変更履歴をオンライン上で預かってくれる
- プルリクエストでの複数人開発変更の取り込み・修正・改善
- 世界中のチームがGitHub上で開発グローバル開発のプラットフォーム
- Bitbucket という競合がある。GitHubと同じようなホスティングシステム
### Gitはスナップショットで保存している
- fileをそのまま保存している。差分を保存しているわけではない
- 下記を確認　↓　verごとに、その時のA、Bの状態をそのまま状態で保存
| ver1  | ver2  | ver3  |
| :---: | :---: | :---: |
|   A   |  A1   |  A2   |
|   B   |  B2   |  B2   |
>verを記録することでコミットをたどれば以前の状態に戻せる。スナップで保存しているので出来る事。git以前は差分として情報管理していたので merge するのにとても時間がかかっていた。
- commit　＝　commit がverを記録している。
   - 1つ前の commit の親情報も保持している
## Git Bash 初期設定
#### 登録
- $ `git config --global user.name "Git Hub user name"`
- $ `git config --global user.name "Git Hub user email"`
- $ `git config --global core.editor " userの使用エディタ --wait"`
#### 確認
- $ `git config user.name` 　　　ユーザー名
- $ `git config user.email`　　　メールアドレス
- $ `git config core.editor`　　 git使用エディタ（ソフト）
- $ `git config --list`　　　　　　登録されている全ての内容確認　
- $ `cat ~/.gitconfig`　　　　　　fileの中身を表示
## ワークツリー　 [fileを変更する作業場所]
#### 自分がコードを記述して作業している場所事を指す
- コードを記述している場所　＝　ワーク　
- ディレクトリやフォルダー　＝　ツリー
## ステージングエリア　[コミットする変更を準備する]
#### 複数fileを変更したときに、コミットするfileを選択する為にあるエリア

★ コード記述
- $ `git add <file名>`　　　　　　file名をステージング
- $ `git add.`　　　　　　　　　　ステージングエリアに全部追加
## ローカルリポジトリ　[スナップショットを記録　コミット]
### .git (隠しファイル)
>fileやディレクトリを状態、変更履歴を記録する自身のPCの場所。
### commit (コミット)　Gitの根幹
>コミットして変更をローカルリポジトリに記録。原則ひとつの作業ごとに１コミット。変更にメッセージを付けてリポジトリに記録する。そうする事によってリポジトリ内で時系列でfileが記録され管理がとてもしやすい。

★ コード記述
- $ `git commit`　　　　　　　　　　　コミット
- $ `git commit　-v`　　　　　　　　　コミットするfile変更点参照
- $ `git commit　-m ファイル名`　　　　参照なしver・コメント有り

★ 分かり易い commit メッセージを書く（メンバー共有の為）
- １行目　変更内容の要約`
- ２行目　空行
- ３行目　変更した理由
### push (プッシュ)
>リモートリポジトリにアップする

★ コード記述
>先にローカルリポジトリを作成している場合は．．．
- $ `git remote add origin https://github.com/user/-.git`
- $ `git　push -u origin master`
>※　-u を付けることによって、次回からは　$ `git push` だけに省略できる
## リモートリポジトリに登録
>リモートリポジトリ　＝　GitHub｡リモートリポジトリは複数持つことができる
### リモートリポジトリ表示
★ コード記述
- $ `git remote`　　　　　　登録されているリモートリポジトリ
- $ `git remote -v`　　　　対応URLを表示
### リモートリポジトリ新規追加
★ コード記述
- $ `git remote add` 　　　リモートリポジトリを登録できる
>※ その後記述は origin URL → github.com/user/リポジトリ名.git

>origin → gitでのリモートリポジトリに付けるデフォルトでつける名前
### リモートリポジトリ複数登録
★ コード記述
- $ `git remote add ○○name`　　○○という名前で登録できる
>https:/github.com/user/リモートリポジトリ名.git
- 最初に登録したoriginと別のモノとして、○○という名前で使用していける
- $ `git　push -u ○○name master`　　　プッシュ
>※ 最初に登録したorigin masterの情報が○○のリモートリポジトリ（github上）に反映される
## リモートリポジトリへ送信
#### git push コマンドで、ローカルリポジトリの内容をリモートリポジトリへ送信する
★ コード記述
- $ `git push origin master`
>※ origin デフォルトのリポジト　　master デフォルトブランチ名
## GitHubから情報取得（fetch編:フェッチ）
#### fetchではリモートリポジトリからロールリポジトリに情報を落としてくる。
>※ fetch の意味はとってくるという事
### **ワークツリーに反映されないので注意**
>※ ワークツリー　＝　directoryやfile（コード記述をしているエディタ）など
##### fetch 後ロールリポジトリからワークツリーに情報を反映させる
- $ `git merge`

★ コード記述
1. $ `git fetch リモートリポジトリ○○名`　 　　　情報取得
2. $ `git branch -a`　　　　　　　　　　　　　　　今自分がいるブランチ名確認
3. $ `git checkout remotes/○○/master`　　　取得したいリモートリポジトリにスイッチ
4. $ `ls`　　　　　　　　　　　　　　　　　　　　　　 ○○fileを確認
5. $ `cat`　　　　　　　　　　　　　　　　　　　　　　○○fileの中を確認
6. $ `git checkout master`　　　　　　　　　　　自分のmasterブランチに戻る
7. $ `git branch -a`　　　　　　　　　　　　　　　今自分がいるブランチ名確認
8. $ `git merge ○○/master`　　　　　　　　　　　情報をワークツリーに取得
9. $ `ls`　　　　　　　　　　　　　　　　　　　　　　　○○リモートリポジトリのデータがある
## GitHubから情報取得（pull編:プル）
>リモートリポジトリから情報を取得して、マージまでを一度にやりたい、ワークツリーにも情報を一気に反映させたい。

★ コード記述
- $ `git pull リモート名　ブランチ名`
- $ `git pull origin master`
>※ 上記は　git pull に省略可能
- $ `git pull`
### git pullは下記コマンドを合わせた意味を持つ
> $ `git fetch origin master　＋　$ git merge origin/master`
## fetch とpull の使い分け
>基本的にはfetchを使用したほうが良い。　pullは楽だが挙動がとても特殊。しっかりgitを理解できて使用できるまではfetchを使用したほうが安全。それか、運用ルールとして自分がmasterのbranchにいて何も変更していない時だけpullを使用するなど。

>※ 他のbranchにいる時は、git pullしても大丈夫か考えないといけない。

### ★ pullの注意点

- $ `git pull origin hoge` 取得　　① リモートリポジトリから
- $ `git pull origin hoge` 取得　　② ロールリポジトリに　　　
- $ `git pull origin hoge` 取得　　　ここが注意! ワークツリーに　　　　　

>※ このワークツリー取得の時に、同じブランチに自分自身がいないと違う情報が統合されてしまう
## リモートの情報詳細を確認したい時
>git remote コマンドよりもより詳しく情報詳細が確認できる
- fetch とpush のURL
- リモートブランチ
- git pullの挙動
- git pushの挙動

★ コード記述
- $ `git remote show リモート名`
- $ `git remote shoe origin`

## リモートを変更・削除
>別のリモート名を使いたくなった時、リモートを使わなくなった時
★ コード記述
#### 変更
- $ `git remote rename 旧リモート名　新リモート名`
#### 削除
- $ `git remote rm リモート名`
## Gitで管理したくないfile
>.gitignore (ギットイグノア) fileに指定する事で、fileをGitの管理から外すことができる。
### .gitignore　(スペルミス注意) / .gitignore がある同じ階層にfileを置く事
- **.gitignore　fileがしっかりと出来た時はエディタ(エクスプローラー)のfile名**
- **.gitignoreの左横にGitのロゴが出る！**
- **管理対象外になったfileは、薄い灰色に変わる！**
- **.gitignoreと同じ階層(同じ場所、同じdirectory内)に管理対象外fileは置く事！**
- **キャッシュの削除！**
- 自動生成されるfile
- パスワードが記載されているfile
- #から始まる行はコメントとした扱いとなる
- 指定したfileを除外　　　　　　　　　　　`index.html`
- ルートディレクトリを指定　　　　　　　　　　`/root.html`
- ディレクトリ以下を除外　　　　　　　　　　`dir/`
- / 以外の文字列にマッチ「*」　 　　　　　　`/*/*.css`
## gitignoreファイルが有効にならない原因
#### 「一度gitの管理対象となっていることが原因」
>具体的には、git commitなどを行いgitの管理対象となっている場合に、ステージングエリア（キャッシュ）に管理対象外としたいファイルが存在する場合は、その状態で.gitignoreに追加しても管理対象外とならないためです。

- $ `git rm -r --cached file名`
- $ `commit  →　push`
※これでgit管理対象外になる。
## コミットしてしまったfileを管理から外す
>git rm コマンドを使用　コミットしたfileをgitの管理から削除できる。

★ コード記述
- $ `git rm ○○file`　　　　　　　　 　　　○○fileも一緒に削除
- $ `git rm -r ○○ディレクトリ`　　 　　　　○○ディレクトリも一緒に削除
- $ `git rm --cached (キャッシュトゥ)`　　fileは残す場合　.gitignoreは追記
## 既存のプロジェクトからGitを始める
>GitHub上にあるプロジェクトからクローンを作る。git リポジトリのコピーを作成する

★ コード記述
1. mkdir ファイル名　　　　　　　　 　　　　　新規ディレクトリ作成
2. GitHub 上に　code　　　　　　　 　　　　clone URL コピー
3. $ `git clone URL`　　　　　　　　 　　ディレクトリにclone作成

>※　少し時間がかかる　１００％になったら完了
4. $ `ls` 又 `get-childitem -force`　　　既存プロジェクトデータ参照
## ファイルの移動/ファイル名の変更を記録
★ コード記述
- $ `git mv <旧file><新file>`　　　　　mv はmoveの略　re name
- $ `.gitignore　development`　　　　　directory → 入れる
- $ `.gitignore　../ `　　　　　　　　　　directory → 出す
>※ 以下のコマンドと同じ
- $ `git mv  <旧file><新file>`
- $ `git rm  <旧file>`
- $ `git add <新file>`
>※　通常のコマンドを使用しても代替えはできる
## コマンドにエイリアスをつける
#### 入力単語を置き換え。短縮。ショートカット。
★ コード記述`
- $ `git config --global alias.ci commit`
- $ `git config --global alias.st status`
- $ `git config --global alias.br branch`
- $ `git config --global alias.co checkout`
- $ `git config` = 設定を変更するコマンド
   - ※ ~/.gitconfig　**今いるプロジェクトの下のfileで適用**
- --global を付けるとHomeディレクトリの下のfile、PC全体の設定を変更するコマンド
   - ※ ~/.config/git/config　　**PC全体の設定になる**
## fileへの変更を取り消す
>元のワークツリー状態に戻したい時、ぐちゃぐちゃになった時etc...
★ コード記述
- $ `git checkout -- file名` 　　　　　　半角スペース忘れずに
- $ `git checkout -- director名`　　　　半角スペース忘れずに
- $ `git checkout -- .（ピリオド）` 　　　全変更を取り消す

>※ “--”を使用しているのは、ブランチ名とファイル名が被った時に、Gitが分からなくなるのを避ける為

- $ `git checkout -- .`
>「現在いるディレクトリ以下の変更を全て取り消す」というのは、「現在いるディレクトリ以下の全てのファイル」を指します。自分が現在いるディレクトリより上のファイルの変更に関しては取り消せない。
## ● ステージした変更を取り消す
>最新のcommit HEADの内容でステージのfile,directorを上書きする。
- $ `git reset HEAD file名`
- $ `git reset HEAD director名`
- $ `git reset HEAD . (ピリオド)`
#### ※　この変更はステージから取り消すだけ！ワークツリーfileには影響与えない

- fileの中身も変更したい場合は上記のコマンド後に下記を入力
- $ `git checkout -- file名`　　　これで入力で取り消す

## ● 直前のコミットをやり直す
#### **リモートリポジトリにpushしたcommitはやり直しはNG**
- $ `git commit --amend`　　　　　直前のコミットをやり直す
#### ※ pushしたcommit内容は上書きされない！
#### ※ 複数人での作業では事故が起こるので要注意。
#### ※ push後の内容修正は忘れずに **commit & push** をセットとする事！！
