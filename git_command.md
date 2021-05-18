# Git command manual
## ターミナルの頻出

- $ `cd`　　　　　ディレクトリを移動
- $ `ls`　　　　　ディレクトリの内容を表示
- $ `ls -a`　　　隠しファイルを含めたディレクトリ全内容を表示
- $ `mkdir`　　　ディレクトリを新規作成
- $ `rm`　　　　　ファイルを削除
- $ `cp`　　　　　ファイルをコピー
- $ `mv`　　　　　ファイルの移動とファイル名の変更
- $ `pwd`　　　　 今自分がいるfileの所在地を表示
- $ `cat`　　　　　ファイルの中身を表示
## Vim
- $ `vim test.txt`　　　　　　　　　tets.txt file作成
- $ `a`　　　　　　　　　　　　　　a = INSERT (挿入) txt入力可
- $ `esc`　　　　　　　　　　　　　入力終了
- $ `:wq`　　　　　　　　　　　　　保存
- $ `vim test.txt`　　　　　　　　　tets.txt file 編集・内容確認
## powershell
- $ `Get-ChildItem`　　　　　　　　lsの代わりになるコマンド
- $ `Get-ChildItem　- froce`　　 　　隠しファイルを含めたディレクトリ全内容を表示します。
- $ `new-item`　　　　　　　　　　　新規file・directory 作成
## ローカルリポジトリ　作成
- $ `mkdir ○○`　　　　　　　　　　　○○directory 新規作成
- $ `git init`　　　　　　　　　　　○○dirで、git dir新規作成（.gitが）ロールリポジトリを管理する
## git 初期設定・確認
### 登録
##### user name
    git config --global user.name "Git Hub user name"
##### user email
    git config --global user.name "Git Hub user email"
##### editor (使用エディタ)
    git config --global core.editor " userの使用エディタ --wait"

### 確認(登録中の情報を表示・参照)
##### user name
    git config user.name
##### user email
    git config user.email
##### editor（使用エディタ）
    git config core.editor
##### 登録されている全ての内容確認
    git config --list　
##### 登録されているfileの中身を表示
    cat ~/.gitconfig
## 基本的なワークフロー

- $ `git status`　　　　　　　　　　現状確認

- $ `git diff`　　　　　　　　　　　　difference の略。
>※　git addとかcommitする前の確認の為に使用
。今のローカルの状態とステージング状態の差分確認
- $ `git diff HEAD`　　　　　　　　ステージング状態と最新commitの差分を確認するため


- $ `git add .`　　　　　　　　　　　全てステージン
- $ `git add　file名`　　　　　　　　選択fileだけステージング

- $ `git commit -v`　　　　　　　　コミット・コメント（エディタが開く）
- $ `git commit -m`　　　　　　　　コミット・コメント（ターミナ上で完結）


- $ `git log`　　　　　　　　　　　　コミット履歴確認

- $ `j → 下 ｋ → 上 ｑ → 終了`　　git log履歴画面での移動コマンド　

- $ `git log --oneline`　　　　　1行で log を表示してくれる
- $ `git log -n3`　　　　　　　　　最新のコミット３つを表示

- $ `git log --oneline -n3`　　　1行で log　表示と最新３つを表示



## file ＆ directory削除

- $ `git rm  ○○file`　　　　 　　　 ワークツリー＆ローカルリポジトリから○○file削除
- $ `git rm  ○○directory`　　　　　ワークツリー＆ローカルリポジトリから○○ディレクトリ削除
- $ `git rm --cached file名`　　　　ワークツリーには file  を残して、ローカルリポジトリは削除

- $ `git commit　-v`　　　　　　　　　rm した事を commit
- ↑　最後に必ず **commit** 忘れずにやる事！！

#### **何故　rm 後に　commit をし直すのか？**
>git rm コマンドを実行すると、ステージにfile削除が記録されます。それを commit するとローカルリポジトリからも削除されるというのが正確な挙動になる。git rm コマンド自体は「ファイルの削除をリポジトリに記録する」ためにあり、挙動としては「ステージにファイルの削除を記録する」

## ファイルの移動/ファイル名の変更を記録

- $ `git mv <旧file> <新file>`　　　　　　　ファイル名変更　（re name）

- $ `git mv <file名> <directory名>`　　　　file → directory へ移動

- $ `git mv directory名/ .gitignore`　　　directoryから → fileを出す



## コマンドにエイリアスをつける
>入力単語を置き換え。短縮。ショートカット。よく使うコードは置き換えたほうが良い
#### エイリアス
##### commit　→　ci
    git config --global alias.ci commit
##### status　→　st
    git config --global alias.st status
##### branch　→　br
    git config --global alias.br branch
##### checkout　→　co
    git config --global alias.co checkout
### git config = 設定を変更するコマンド
- ※ ~/.gitconfig　　今いるプロジェクトの下のfileで適用

- --global を付けるとHomeディレクトリの下のfile、PC全体の設定を変更するコマンド
   - ※ ~/.configit/config　　PC全体の設定になる
## Gitで管理したくないfile

#### .gitignore　(スペルミス注意)
    .gitignore
- .gitignoreの左横にGitのロゴが出る！

## gitignoreファイルが有効にならない原因
#### **「一度gitの管理対象となっていることが原因」**
>具体的には、git commitなどを行いgitの管理対象となっている場合が多い。ステージングエリア（キャッシュ）に管理対象外としたいファイルが存在する場合は、その状態で.gitignoreに追加しても管理対象外とならないためです。
##### キャッシュ削除
    git rm -r --cached "file名"
##### 削除を commit
     git commit -v
##### ローカル(master)とリモート(origin)情報を揃える
     git push
#### これでgit管理対象外になる。
## fileへの変更を取り消す
>元のワークツリー状態に戻したい時、ぐちゃぐちゃになった時etc...
##### file
    git checkout -- "file名"
##### directory
    git checkout -- "directory名"
##### 現在いるdirector以下/全変更を取り消す
    git checkout --　.
>※ “--”を使用しているのは、ブランチ名とファイル名が被った時に、Gitが分からなくなるのを避ける為
## ステージした変更を取り消す
>最新のcommit HEADの内容でステージのfile,directorを上書きする。
##### file
    git reset HEAD "file名"
##### directory
    git reset HEAD "director名"
##### ステージングしてあるモノ全て
    git reset HEAD .
#### **この変更はステージから取り消すだけ！ワークツリーfileには影響与えない！！ワークツリーの変更・編集内容はそのままなので安心して下さい。**

>※ fileの中身も元に戻したい場合は上記のコマンド後に下記を入力後に下記のコード使用
##### fileへの変更を取り消す
    git checkout -- file名
## 直前のコミットをやり直す

### **リモートリポジトリにpushしたcommitはやり直しは絶対NG**
>※ 必ずコンフリクトが起こる！！！
##### 直前のコミットをやり直す
    git commit --amend
#### ※ pushしたcommit内容は上書きされない！
#### ※ 複数人での作業では事故が起こるので要注意。
#### ※ push後の内容修正は忘れずに **commit & push** をセットとする事！！
