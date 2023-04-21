# はじめてのQuay.io

Red Hatのコンテナレジストリ「Quay.io」にアカウントを作り、コンテナをpushしてみましょう。
Quayは「キー」と呼ぶそうです。

## Quay.ioでアカウント作成
Red Hatアカウントを持っている人がQuay.ioにはいって操作

https://docs.quay.io/solution/getting-started.html

### Quay.io を使い始める
https://quay.io にアクセスします。

右上のSIGN INをクリックしてください。

注) 「Try for Free on Cloud」をクリックしないで下さい

Red Hat アカウントの SSO ページが表示されたら、自身のRed Hat アカウントを入力して下さい。

Help!) かわのはすでにこの作業を終えていて、どんな手順で利用可能になったか覚えていません。だれか画面共有して見せて&画像ください

### Quay.io にサインインする
コンソール作業に戻ります。loginコマンドでサインインします。
```
podman login quay.io
```

ユーザ名とパスワードを求められるので、Quay.ioで設定した情報を入力します。

### 新しいコンテナを作成する
コンテナイメージ ubuntu を実行し、新しいファイルを含むコンテナを新たに作成します。

```
podman run ubuntu echo "fun" > newfile
```
コンテナはすぐに終了します。psコマンドでコンテナIDを表示し、どこかに書き留めましょう。(次で必要になります)

```
podman ps -a
```

### コンテナーをイメージにタグ付けする
次に、コンテナーを既知のイメージ名にタグ付けする必要があります

```
podman commit <container id> quay.io/<username>/<reponame>
```

`<container id>`: 先ほど書き留めたコンテナID<br/>
`<username>`: Quay.io のユーザ名<br/>
`<reponame>`: 新しく作成したコンテナの名前


### コンテナイメージを Quay.io にプッシュする
```
podman push quay.io/<username>/<reponame>
```

これで、コンテナイメージがコンテナレジストリに登録されました。

### Quay.io からイメージをダウンロードする
他のユーザがpushしたイメージをpullしてrunしてみましょう！
