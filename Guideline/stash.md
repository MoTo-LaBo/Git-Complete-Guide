# stash について
#### 作業が途中でコミットしたくないけど別のブランチで作業をしないといけない時、stash へ一時避難させる
    git stash
#### stash は「隠す」という意味
- $ `git stash save`
>※　save　はついて無くても意味は同じ
#### 避難した作業の一覧を表示
    git stash list
## 一時避難した作業を復元
>※ 作業は復元されるが、ステージングの状況までは復元されない
#### 最新の作業を復元
    git stash apply
#### ステージングの状況も復元
    git stash apply --index
#### 特定の作業を復元する
- $ `git stash apply スタッシュ名`
- $ `git stash apply stash@{1}`
## 避難した作業を削除する
#### 最新の作業を削除
    git stash drop
#### 特定の作業を削除
- $ `git stash drop スタッシュ名`
- $ `git stash drop stash@{1}`
#### 全作業を削除
    git stash clear

