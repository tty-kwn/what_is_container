# Podman Desktop のインストール と　Podmanコマンドの使い方

## Podman Desktop for Windows のインストール
**公式ページ**：[Windowsインストーラを使って Podman Desktop をインストールする方法](https://podman-desktop.io/docs/Installation/windows-install)

以下、軽く解説(更新されているかもしれないので、インストールがうまくいかない場合は最新内容をチェックして下さい)

* とりあえずインストールしたい人
  * [インストーラダウンロードページ](https://podman-desktop.io/downloads/windows)から「Download Now」でインストーラをダウンロード
  * インストーラを実行、全てデフォルトのまま「はい」で進めてOK
* インストールせずに実行したい人
  * [インストーラダウンロードページ](https://podman-desktop.io/downloads/windows)で「Windows portable executable」をクリックして、exe本体をダウンロード
* サイレントインストールしたい人(管理者がユーザに黙ってインストールさせたりとか)
  * https://podman-desktop.io/docs/Installation/windows-install/installing-podman-desktop-silently-with-the-windows-installer)
* パッケージマネージャを導入している人
  * `choco install podman-desktop`
  * `scoop bucket add extras　&& scoop install podman-desktop`
  * `winget install -e --id RedHat.Podman-Desktop`
* インターネットが使えない制限された環境の人
  * https://podman-desktop.io/docs/Installation/windows-install/installing-podman-desktop-and-podman-in-a-restricted-environment
  * インストール時にダウンロードするライブラリ等一式含まれている版。

### Podman のインストール
Podman DesktopはあくまでGUI。Podman engineの導入が別途必要です。
Windowsの場合、Podman engine自体は仮想マシン上のLinuxで動作させる必要があります。

1. PowerShell画面を管理者権限で起動
2. WSLをLinux(デフォルトUbuntu)抜きでインストール
   * wsl --install --no-distribution
3. Podman Desktopで「Install」ボタンクリック
4. Podmanインストーラは全てデフォルトのままインストールしてしまう
5. 「Initialize Podman」ボタンクリック。
   * `podman machine init && podman machine start` をおこなってくれている 

## Podman Desktop for mac のインストール
1. Podman Desktop ARM版（DMG）のダウンロードとAppへのコピー
   * https://podman-desktop.io/downloads/macos からARM版のリンクをクリック
2. Podman Installボタン実行
3. Mac画面上部のPodman常駐クリックメニューのdashboardで開いた画面の右側のinstallボタンをクリック
4. MacのTerminal起動
5. Homebrewのインストール
   * /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
6. brew install podmanの実行
7. podman machine initの実行
8. podman machine startの実行

## Podman 動作確認
### Hello World
```
podman run hello-world
```

以下が出力されればOK
```
!... Hello Podman World ...!

         .--"--.
       / -     - \
      / (O)   (O) \
   ~~~| -=(,Y,)=- |
    .---. /`  \   |~~
 ~/  o  o \~~~~.----. ~~
  | =(X)= |~  / (O (O) \
   ~~~~~~~  ~| =(Y_)=-  |
  ~~~~    ~~~|   U      |~~
```
Quay.ioからhelloという名前のコンテナを持ってきて(pull)、自分のpodman engine環境で実行した結果です。

podmanのアイコンを素敵なアスキーアートで表現していますね。

### podman コマンド実行
いろいろ実行してみましょう。

![lifecycle](./images/image1.png)

#### 1. コンテナ実行前の事前ダウンロード(podman pull)


```
podman pull docker.io/nginx
```

```
podman pull quay.io/quay/busybox
```

#### 2. ダウンロードしたコンテナイメージの確認(podman images)

```
podman images
```

pullしたイメージがリストアップされていますね

#### 3. コンテナの実行(podman run)

```
podman run -it --name test1 busybox sh
```

* どういう状態?: 
  * busyboxコンテナをtest1という名前で作成、(-itオプションで)接続し、コマンド実行可能な状態になっています。ls, pwd, echo コマンドなどお試しください。
* 停止：
  * `exit`と入力しEnterしてください。

#### 4. コンテナの状態の確認表示(podman ps)
実行中コンテナの状態を確認します。

```
podman ps
```

1つもありません。

続けて、停止状態を含めたコンテナの状態を確認します。

```
podman ps -a
```

起動したコンテナが停止状態にあることがわかります。

#### 5. デーモンコンテナの実行(podman run)

```
podman run -d --name docker-nginx -p 8080:80 docker.io/nginx
```

* どういう状態?:
  * 8080ポートでnginxというWebサーバが起動しhttpリクエストを8080ポートで待っている状態です。
  * ブラウザで　http://localhost:8080 にアクセスしてください。nginxのデフォルトページが表示されます。

```
podman ps
```

namesがdocker-nginxのコンテナが表示されています。
docker-nginxが起動中ということです。
もう一度ブラウザで　http://localhost:8080 にアクセスしてください。やはりnginxのデフォルトページが表示されます。

#### 6. ログの確認(podman logs)

コンテナのログを確認できます。

```
podman logs docker-nginx
```

このログは、標準出力(stdout)と標準エラー(stderr)へ書き出されたデータです。
Linuxの`tail -f`と同様に、-fオプションを付けることで稼働しているコンテナのログをリアルタイムに確認できます。

以下を実行したら、もう一度ブラウザで　http://localhost:8080 にアクセスしてみてください。

```
podman logs -f docker-nginx
```

ログにアクセスログが出ましたか？ 出ない方はブラウザをリロードしてみてください。

#### 7. コンテナの停止(podman stop / podman kill)

docker-nginxプロセスを停止しましょう。

```
podman stop docker-nginx
```

```
podman ps -a
```

docker-nginxコンテナのSTATUSがExited(停止)となっています。つまり、停止させることができました。

ちなみに、podman stopと同じくコンテナプロセスを停止する役割としてpodman killがあります。
podman stopはSIGTERM(プロセス通常停止)でコンテナプロセスを停止しますが、podman kill は SIGKILL(強制停止)でプロセスを停止しています。
通常はpodman stopでプロセスを停止し、それで止まらない場合、異常時などにkillを使うようにしましょう。

#### 8. コンテナの起動(podman start)

止めた docker-nginx コンテナを起動します。

```
podman start docker-nginx
```

```
podman ps -a
```

docker-nginxコンテナのSTATUSがUp(起動)になっています。つまり、起動できました。

もう一度ブラウザで　http://localhost:8080 にアクセスしてください。nginxのデフォルトページが表示されます。

#### 9. コンテナの削除(podman rm)

使わないコンテナを削除します。

```
podman rm docker-nginx
```

エラーが表示されました。起動中のコンテナは、一度停止してから削除できます。
(Linuxのrmコマンドと同じく、**-f** オプションで強制的に削除可能です)

では、すでに止まっている他のコンテナを削除しましょう。

```
podman rm test1
```

```
podman ps -a
```

`ps -a` のリストから test1 コンテナが消えました。


#### 10. ローカルリポジトリからコンテナイメージの削除(podman rmi)

test1 コンテナはコンテナプロセスとしては削除しましたが、イメージ自体は残っています。

```
podman images
```

このイメージさえも削除してみましょう。

```
podman rmi quay.io/quay/busybox
```

```
podman images
```

消えましたね。これでローカルリポジトリからイメージさえも消えました。
次回利用する際は、再度Quay.ioからダウンロードしローカルリポジトリに保存した上でコンテナ起動、という流れになります。