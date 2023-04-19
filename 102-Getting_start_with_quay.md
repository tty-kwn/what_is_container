# はじめてのQuay.io

Red Hatのコンテナレジストリ「Quay.io」にアカウントを作り、コンテナをpushしてみましょう。
Quayは「キー」と呼ぶそうです。

## Quay.ioでアカウント作成
Red Hatアカウントを持っている人がQuay.ioにはいって操作

https://docs.quay.io/solution/getting-started.html

### Quay.io にサインインする
podman login quay.ioコマンドを実行します。

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

<container id>: 先ほど書き留めたコンテナID
<username>: Quay.io のユーザ名
<reponame>: 新しく作成したコンテナの名前


### コンテナイメージを Quay.io にプッシュする
```
podman push quay.io/<username>/<reponame>
```

これで、コンテナイメージがコンテナレジストリに登録されました。

### Quay.io からイメージをダウンロードする
他のユーザがpushしたイメージをpullしてrunしてみましょう！
