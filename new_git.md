# Git 入門講座
分散型管理システム
### GitHub remoteリポジトリ作成
- リポジトリの名前は - (ハイフン)で区切るのが一般的な規則になっている
### Branch の命名規則
- master が今 main branch に変わってきている
   - master-slave というところから語源がきているので、差別用語的になってしまうということで…
> ※ 今ではGitHub の dfault で main branch に変更されている。GitHubの最高経営責任者 (CEO) であるナット・フリードマン（Nat Friedman）は、5000万人の開発者が利用している同社の用語を中立的なものに変更していると述べた。プログラミング用語では、｢マスター（主人）｣とは、｢スレーブ（奴隷）｣と呼ぶ他のプロセスを制御するメインのコードのこと。置き換え後は｢マスター｣は｢メイン｣、｢スレーブ｣は｢レプリカ｣になる。
### SSH key
`2021年8月13日以降、ローカルリポジトリからリモートリポジトリへアクセスする際にpassword認証ができなくる`
#### ローカルからGitHubへのアクセス方法
- トークン
- SSH
- ２FA
- OAuth
## 1. SSH key をローカルに作成
#### 1.
    ssh-keygen -t ed25519 -C "<GitHub user.email>"
- SSH key が　~/.ssh/ここに２つ作成される
   - (/Users/user/.ssh/id_ed25519)
   - ~/.ssh/id_ed25519 id_ed25519.pub
> ※ pub が公開鍵！！ 間違えないように
#### 2. passphrase (empty for no passphrase): パスフレーズを聞かれる
- ここはpassphraseを使っても使わなくてもいい
- passphraseを使用した場合は２回入力する
#### 3. /Users/user/.ssh/に移動してkeyを確認
    cd ~/.ssh/
#### 4. keyを確認
    ls
- id_ed25519　　id_ed25519.pub
#### 5. ssh-agent 起動させる
    .ssh % eval "$(ssh-agent -s)"
#### 6. .ssh % code ~/.ssh/config ※ editer で~/.ssh/configを編集
    .ssh % code ~/.ssh/config
#### 7. config file に下記を記述
    Host *
      AddKeysToAgent yes
      UseKeychain yes
      IdentitiyFile ~/.ssh/id_ed25519
#### 8. SSH key を ssh-agent に登録する
    ssh-add -k ~/.ssh/id_ed25519
- Identity added: /Users/user/.ssh/id_ed25519 (github user.email)
   - 上記が出れば登録完了！
   - passphrase を登録した人はここで入力がある
## 2. SSH key を GitHub に登録
#### 1. 先ほど上記で作成した公開鍵をクリップボードへcopy
    pbcopy <~/.ssh/id_ed25519.pub
#### 2. GitHub へ公開鍵を登録
- GitHub 上で setting -> SSH and GPG keys -> SSH keys に公開鍵をペースト
