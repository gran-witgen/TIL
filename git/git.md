# Gitについてまとめる  

- gitって？  

バージョン管理  

ファイルの最新状態がわかり、いつだれが何を変更したかわかる。  

- ユーザーの登録  

gitをインストールした状態で、windowsのgit bashより以下を入力  

```
ユーザー登録
git config --global user.name "github user <your_account_name>"

メールアドレス登録
git config --global user.email <your_mail_address>

gitを扱う際のデフォルトのエディタを設定する
ここではvisual studio codeを選択
git config --global core.editor "code --wait"

それぞれの設定が完了したか確認する

git config user.name
git config user.email
git config core.editor

gitに関する情報を一覧として表示する
git config --list
```


