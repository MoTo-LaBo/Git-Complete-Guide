# rebase とは？
#### 変更を統合する際に、履歴をきれいに整える為につかう
- git rebase ブランチ名 →　取り込みたい brach名
- rebase となる branch の親 commit を新しくしている

>　ブランチの基点となるコミットを別のコミットにいどうする
#### 一連の流れ
1. $ `git checkout feature`　　　feature へ移動
2. $ `git rebase master`　　　　rebase master を指定
3. $ `git checkout master`　　　master へ移動
4. $ `git merge feature`　　　　feature を merge する
## ※ git config --global merge.ff false　設定にしておく
#### merge でなぜコメントを残せるような設定にするか？　
>他の branch で作業したらその作業の履歴を残す為

- Fast Foward →　rebase
>※すると何処まで作業したか分からなくなる時があるから上記の様な対策をとっている
- branch での作業履歴を確認したい場合は　**※上記の設定をしておく**
- 上記の流れにする事によって下記と同じ形になる
#### **Fast Foward : 早送りになるマージ**
master の先にあるブランチを merge したとき。枝分かれせずにブランチのHEAD(ポインタ)を前に進めるだけになる
## rebase と merge の違い
- 履歴が枝分かれしているか、一直線であるか
- 親 commit が１つか、２つか
## rebase でしてはいけない事
#### **GitHub に push した commit を　rebase するのは絶対NG**
>※ push が出来なくなる　　push 出来ないからといって　↓
#### 「git push -f　は　絶対NG →強制 push をしてしまうとgitのデータが壊れてしまう」
## merge と rebase の使い分け
#### merge　→　作業の履歴を残したい場合使用
- コンフリクトの解決が比較的簡単　→　コンフリクトが1度しか発生しない
>※　ツリーが枝分かれしているから
- マージコミットが沢山あると履歴が複雑化する
#### rebase　→　作業の履歴を残したくない、キレイ
- 履歴をきれいに保つ事ができる
- コンフリクトの解決が面倒　→　コンフリクトの発生が各 commit ごと発生という挙動が起きる
>※　ツリーが直線的なっているから
#### push していないローカルの変更には　→　rebase
#### push 後は必ず →　merge　　　コンフリクトも　merge
## pull には merge型と rebase型がある
#### **rebase型の使用がオススメ**
- $ `git pull --rebase リモート名　ブランチ名`
- $ `git pull --rebase origin master`

**merge commit が残らない**ので、GitHub の内容を取得したいだけの時は **--rebase** を使用
#### pull を rebase型に設定する
**--rebase** オプションを付けなくても　git pullの挙動が rebase型になる
- $ `git config --global pull.rebase true`
#### master branch で git pullする時だけ ↓
- $ `git config branch.master.rebase true`
#### こういった設定をすると何処に保存されるのか？
ローカルのPC　home directoryの中　下記参照　↓
#### -- global を付けるとPC全体の設定になる
- `~/.gitconfig`
- `~/.config/git/config`
#### --global を付けないと　今の project だけでの設定になる
- `ロカールリポジトリ`　
- `project/.git.config`
## rebase で履歴を書き換える
#### コミットをキレイ整えてから push したいときは履歴を書き換える
>※　GitHub に push していない commit に限る！
- $ `git commit --amend`
- 上記は直前の commit をやり直す
>※ リモートリポジトリに push した commit はやり直してはいけない！　
#### 複数の commit をやり直す
- $ `git rebase -i コミットID`
- $ `git rebase -i HEAD~3`　：　直近の３つの　commit が表示される
- pick ○○○id　ヘッター修正
- pick ○○○id　fileの追加
- pick ○○○id　.txtの修正
-  -i は　--interactive の略。対話的 rebase といって、やり取りしながら履歴を変更していく
#### やり直したい commit を edit に変更する
- **edit** ○○○id　ヘッター修正
- pick ○○○id　fileの追加
- pick ○○○id　.txtの修正
#### やり直したら実行する
- $ `git commit --amend`　で commit のコメント編集
#### 次の commit に進む (rebase完了)
- $ `git rebase --continue`
#### ※ git rebase --edit-todo　というコマンドもある
>これは使用中のエディタが立ち上がり rebase の編集ができる。（vs code　拡張機能有での話）
## rebase commit を並び替え・削除
#### commit をまとめる
#### squash を利用。複数のある commit をまとめる
- $ `git rebase -i head~3`
- エディタで commit を編集
1. pick　新規作成
2. pick　test.txt 作成
3. pick　index.html　作成
>※　上記のようになっているので
- まとめたいfileは　pick のままにしておくその他は squash に変更
1. pick　新規作成
2. **squash**　test.txt 作成
3. **squash**　index.html　作成
- git log --oneline で確認すると下記のような履歴変更になる
#### 「 1747d71 (HEAD -> master) 新規作成 」
## commit を分割する
#### まとめて commit してしまったモノを修正して１つの commitに分割。
>※ 上記の例を使用　↑
- $ `git log --oneline` で確認すると下記のような履歴
#### 「 1747d71 (HEAD -> master) 新規作成 」
- $ `git rebase -i head~3`
>※　エディタで下記の様な commit 履歴が立ち上がる ↓

1. pick　新規作成
2. pick　test.txt 作成
3. pick　index.html　作成
- **edit** に変更する　↓
1. **edit**　新規作成
2. pick　test.txt 作成
3. pick　index.html　作成
- $ `git reset HEAD^`　　↓

>※ commit の取り消しと、ステージングの取り消しになる
- $ `git status`
1. frist.txt
2. test.txt
3. index.html

　例）その後の一連の流れ
1. $ `git add fist.txt`
2. $ `git add test.txt`
3. $ `git commit -m fist.txtとtest.txtを追加`
4. $ `git add index.html`
5. $ `git commit -m index.htmlを追加`
6. $ `git rebase --continue`
7. $ `git push`
8. これで次の rebase 作業に進んで行ける
