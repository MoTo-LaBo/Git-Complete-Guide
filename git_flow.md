# git-flow
- ソフトウェアの開発ではよく使われる
- git に 5つの branch を作成して運用していく
- 他の人に悪影響を与えない
- 何かあった時でもその branch を削除すれば元に戻せる

## ★ master branch
- 開発中は一切触る事はない
>※ release branch・hotfix branch から merge される事くらい
## ★ develop branch
普段は develop branch で開発する
## ★ featur branch
featur branch が一番使用頻度が高い。開発のメインの場所
## ★ release branch
リリース前に詳細 test などをしていく為の所
## ★ hotfix branch
bug 修正専用の branch
master branch からしか branch はきらない
>※ そうする事で develop での開発しながら、 master では公開しながら作業ができる
完了したら、 tag を付けて master と develop へ　merge させる
>※ merge する時は必ず checkout してから merge する事
## ● 運用の一連の流れ
#### 1. develop branch もそんなに開発では手を加えない
ではやりたい事があった時に開発はどうするか？ featur branch へ branch をきる
#### 2. featur / bilud_top_page という形で featur で開発をしていく
それぞれで featur branch を使って開発していく
#### 3. test などをして完成したら develop branch へ merge をしていく
featur branch は残さなくて大丈夫
#### 4. 1 ~ 3 の繰り返しで、リリース準備ができたら release branch へ branch をきる
#### 5. test の中で bug などが見つかって直していく
#### 6.release branch で完成したモノを master へ merge
>※ master を checkout してから merge
#### 7.release branch で完成したモノは develop へも merge
>※ develop を checkout してから merge
release から develop へも merge する事で足並みが揃う
#### 8. 最新の develop branch から featur へ branch をきる事で最新の開発ができる
### ソフトウェア開発では使われているが．．．
- 5つの branch という複雑さがある
- ここまでは必要がない。特に wed site などの制作場面においては．．．
- これを簡素にして分かり易くしたものが **GitHub - flow**
