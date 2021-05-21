# SSH key 登録

#### 1. 既存のSSHキーが存在するかどうかを確認
    ls -al ~/.ssh　　　　　　
#### 2. default では公開鍵のファイル名は次のいずれか
- id_rsa.pub
- id_ecdsa.pub
- id_ed25519.pub
#### 3. SSH key の生成
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
#### 4. 鍵のfile名・passphrase 生成
- Generating public/private rsa key pair.
  - 公開/秘密RSA鍵ペアを生成中
- Enter file in which to save the key (/c/Users/○○○/.ssh/id_rsa):″file名○○○"
  - ※　ここではfile名 `id_rsa_github` にする
  - ※　`id_rsa` ← default file名
  - キーを保存するファイルを入力します
- Enter passphrase (empty for no passphrase):"passw○○○"
  - パスフレーズを入力します（パスフレーズがない場合は空）
- Enter same passphrase again:"passw○○○"
  - 同じパスフレーズをもう一度入力
>※ passphraseが無くてもGitHubには接続できるようになる。しかし、何かしらの拍子でSSH key の秘密鍵を流失してしまったら GitHub access が簡単に出来てしまう。passphrase を生成しておくと、秘密鍵流失という万が一の事があっても passphrase がないので GitHub access は出来ない。
#### 5. 鍵が出来ているか確認
- `ls`　　　　　　　　　　　　　　鍵を確認
  - id_rsa_github　　　　　　秘密鍵
  - id_rsa_github.pub　　　　公開密鍵
#### 6. 公開鍵を GitHub へ登録する
    cat id_rsa_github.pub
#### 7. 鍵情報をコピー ※ 下記は例です
`ssh-rsa AAAAAAAADAQABAAACAQDTqqbnqj2qo8MMQK7cqyiAcS3QV8J7FcL5pZDgnSNu7yxECAJQr4/+C5OvqrzqDDEhcffj9WpUk+iDrjAD7bz0Kk4EaBj5S+0AhzoR2uJFC6TcHHVG3RIP4hx09149XotQNjPtkoFuAsYWF3UUOnqGsFs5uIdKP3pWkpM0gLUhtJZRPY1SE8T8/0m0WjBHZNKabcM9f0X.com`
#### 8. SSH keys にペースト
`ssh-rsa AAAAAAAADAQABAAACAQDTqqbnqj2qo8MMQK7cqyiAcS3QV8J7FcL5pZDgnSNu7yxECAJQr4/+C5OvqrzqDDEhcffj9WpUk+iDrjAD7bz0Kk4EaBj5S+0AhzoR2uJFC6TcHHVG3RIP4hx09149XotQNjPtkoFuAsYWF3UUOnqGsFs5uIdKP3pWkpM0gLUhtJZRPY1SE8T8/0m0WjBHZNKabcM9f0X.com`
#### title → Add SSH key →　pass でGitHubは key (公開鍵)登録完了！
#### 9. GitHub と接続 test
    ssh -T git@github.com -i ~/.ssh/id_rsa_github
#### 10. 下記ような警告が表示される場合がある。 無ければ 11. へ
The authenticity of host 'github.com (13.114.40.48)' can't be established.RSA key fingerprint is `SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8`.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?`ここに上記公開鍵指紋をコピー＆ペースト`後に enter
#### 11. Enter passphrase for key ' に passphrase 2回入力
>※ passphrase は入力中は表示されない
#### 12. Hi user name! You've successfully authenticated, but GitHub does not provide shell access.
> 上記のコメントが表示され、接続 test 完了!!
#### 13. 設定fileを作成 ※ win なので vs code で作成していく
    code config
#### 14. 下記の情報を入力
- Host github.com
  -  HostName github.com
  -  IdentityFile ~/.ssh/id_rsa_github
  -  User git
#### 15. 下記のコード入力
    ssh -T git@github.com
>※ Hi user name! You've successfully authenticated, but GitHub does not provide shell access.が表示されれば接続完了！！
#### 16. ls で確認 .SSH の directory には以下３つの file ができる
- config
- id_rsa_github
- id_rsa_github.pub
- ※ known_hosts これも入ってます

#### 17. GitHub に commit を反映させる
##### 01 リモートリポジトリ登録 (origin)
    git remote add origin "ssh の URL"
##### 02 登録出来ているか確認 (origin)
    git remote
##### 03 push する。 ※　初回は -u を付ける次からは git push でok
    git push -u origin master
##### 04下記が表示されるので、**passphrase** を入力
Enter passphrase for key '/c/Users/○○○/.ssh/id_rsa_github':**passphrase**
##### 05 ハッシュ値の確認
    git log
- log 上の commit　　f4635......
- remote 上の　　　　f4635......　　両方同じであれば完了！！！
# SSH-agent に追加 (win ver)
**SSH-agent に追加することで push 毎の passphrase 入力を省略できる**
#### 1. sh-agentbashまたはGitシェルを開くと自動的に実行できます。次の行をコピーして、Gitシェルの~/.profileまたは~/.bashrcファイルに貼り付けます。
##### ~/.bashrcファイルを vs code で開く
    code ~/.bashrc
##### 下記リンクのコードを ~/.bashrcファイル
>- https://docs.github.com/en/github/authenticating-to-github/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows
#### 2. ~/.bashrcファイルに貼り付け & 保存完了したら下記入力
    eval `ssh-agent -s`
##### 上記の入力後 Agent pid ○○○数字が表示される
#### 3. SSH秘密鍵をssh-agentに追加
    ssh-add ~/.ssh/id_rsa_github
##### id_○○○　←　(ここは自身が設定した名前に置き換え)

#### test で何かを push してみる。passphraseの入力は求められない。完了！
