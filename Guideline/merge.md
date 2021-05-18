# merge とは？
マージは他の人変更内容を自分のブランチ取り込む　＝　統合する
### merge は master を checkout してする事！！！

- git merge ブランチ名
- git merge リモート名/ブランチ名
- git merge origin master

## merge には3種類ある
#### ● **Fast Foward : 早送りになるマージ**
master の先にあるブランチを merge したとき。枝分かれせずにブランチのHEAD(ポインタ)を前に進めるだけ
#### ● **Auto Merge : 基本的なマージ**
master と feature の２つのブランチがあり、枝分かれしてる時。マージコミットという新しいコミットを作る
#### ● **Contlict(コンフリクト)**
複数人の人が同じカ所で別々に編集をしてしまった時に起きる事象

>例）git merge feature 下記が表示された

>Auto-merging index.html
>CONFLICT (content): Merge conflict in index.html
>Automatic merge failed; fix conflicts and then commit the result.
#### **both modified : index.html**が表示される
- エディタで編集＆修正　→　保存
- git add →　git commit -v →　git log oneline で確認

## ★ コンフリクトの防止策
- 複数人で同じfileを編集しない・変更しない
- pull や merge する前に変更中の状態をなくしておく（commit,stashをしておく）

>※ 変更中のfileがある場合、pull や mergをして、同じカ所でダブルとpull や mergeができなくなる。

- pull する時は、pull するブランチに移動してから pullする

>※　今いるブランチと pullするブランチが同じかを必ず確認する

- コンフリクトしても慌てない

>※　慌てずにゆっくり解決していけば、コンフリクトは解消できる
#### editor に表示される説明文をしっかり読んで理解する事！
>※ エディタは頭がいいので解決方法の提示 ＆ 改善の為のコード提示もしてくれる
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
　**merge の commit が残る**から、 merge したという記録を残した場合に使用
- git pull リモート名　ブランチ名
- git pull origin master

