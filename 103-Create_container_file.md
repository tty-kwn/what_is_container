# Containerfileを作ってみよう
## HelloWorld
任意のフォルダにContainerfileというファイルを作ります。
例えば、
```
mkdir ~/work/103
cd ~/work/103
echo "Hello World" > messagefile
vi Containerfile
```

Containerfileには、以下を記載します。
```
FROM fedora
RUN yum -y update && yum -y install figlet
ADD ./messagefile /messagefile
CMD cat /messagefile | figlet
```

Containerfileのコマンド説明は下記参照。

https://qiita.com/mintak21/items/a6766e3efd6730c9519d

DockerfileもContainerfileも同じ。「Podman」なので「Docker」fileではなく「Container」file。

ビルド実行
```
podman build --tag hw:1.0 .
```

<details>
<summary>実行例 (yumによるインストールがほとんど)</summary>

```
$ podman build .
STEP 1/4: FROM fedora
STEP 2/4: RUN yum -y update && yum -y install figlet
Fedora 38 - x86_64                              3.0 MB/s |  66 MB     00:21
Fedora 38 openh264 (From Cisco) - x86_64        1.4 kB/s | 2.5 kB     00:01
Fedora Modular 38 - x86_64                      1.4 MB/s | 2.3 MB     00:01
Fedora 38 - x86_64 - Updates                    2.9 MB/s | 7.1 MB     00:02
Fedora Modular 38 - x86_64 - Updates            388  B/s | 257  B     00:00
Last metadata expiration check: 0:00:01 ago on Sun Apr 16 07:01:24 2023.
Dependencies resolved.
================================================================================
 Package             Architecture  Version                 Repository      Size
================================================================================
Upgrading:
 libgcrypt           x86_64        1.10.2-1.fc38           updates        514 k
 libgpg-error        x86_64        1.47-1.fc38             updates        230 k
 python3             x86_64        3.11.3-1.fc38           updates         28 k
 python3-libs        x86_64        3.11.3-1.fc38           updates        9.6 M
 rpm-sequoia         x86_64        1.4.0-1.fc38            updates        851 k

Transaction Summary
================================================================================
Upgrade  5 Packages

Total download size: 11 M
Downloading Packages:
(1/5): python3-3.11.3-1.fc38.x86_64.rpm          96 kB/s |  28 kB     00:00
(2/5): libgpg-error-1.47-1.fc38.x86_64.rpm      676 kB/s | 230 kB     00:00
(3/5): libgcrypt-1.10.2-1.fc38.x86_64.rpm       1.3 MB/s | 514 kB     00:00
(4/5): rpm-sequoia-1.4.0-1.fc38.x86_64.rpm      1.9 MB/s | 851 kB     00:00
(5/5): python3-libs-3.11.3-1.fc38.x86_64.rpm    4.7 MB/s | 9.6 MB     00:02
--------------------------------------------------------------------------------
Total                                           3.8 MB/s |  11 MB     00:02
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1
  Upgrading        : python3-libs-3.11.3-1.fc38.x86_64                     1/10
  Upgrading        : python3-3.11.3-1.fc38.x86_64                          2/10
  Upgrading        : libgpg-error-1.47-1.fc38.x86_64                       3/10
  Upgrading        : libgcrypt-1.10.2-1.fc38.x86_64                        4/10
  Upgrading        : rpm-sequoia-1.4.0-1.fc38.x86_64                       5/10
  Cleanup          : python3-3.11.2-1.fc38.x86_64                          6/10
  Cleanup          : libgcrypt-1.10.1-7.fc38.x86_64                        7/10
  Cleanup          : libgpg-error-1.46-2.fc38.x86_64                       8/10
  Cleanup          : python3-libs-3.11.2-1.fc38.x86_64                     9/10
  Cleanup          : rpm-sequoia-1.3.0-1.fc38.x86_64                      10/10
  Running scriptlet: rpm-sequoia-1.3.0-1.fc38.x86_64                      10/10
  Verifying        : libgcrypt-1.10.2-1.fc38.x86_64                        1/10
  Verifying        : libgcrypt-1.10.1-7.fc38.x86_64                        2/10
  Verifying        : libgpg-error-1.47-1.fc38.x86_64                       3/10
  Verifying        : libgpg-error-1.46-2.fc38.x86_64                       4/10
  Verifying        : python3-3.11.3-1.fc38.x86_64                          5/10
  Verifying        : python3-3.11.2-1.fc38.x86_64                          6/10
  Verifying        : python3-libs-3.11.3-1.fc38.x86_64                     7/10
  Verifying        : python3-libs-3.11.2-1.fc38.x86_64                     8/10
  Verifying        : rpm-sequoia-1.4.0-1.fc38.x86_64                       9/10
  Verifying        : rpm-sequoia-1.3.0-1.fc38.x86_64                      10/10

Upgraded:
  libgcrypt-1.10.2-1.fc38.x86_64        libgpg-error-1.47-1.fc38.x86_64
  python3-3.11.3-1.fc38.x86_64          python3-libs-3.11.3-1.fc38.x86_64
  rpm-sequoia-1.4.0-1.fc38.x86_64

Complete!
Last metadata expiration check: 0:00:12 ago on Sun Apr 16 07:01:24 2023.
Dependencies resolved.
================================================================================
 Package    Arch       Version                                 Repository  Size
================================================================================
Installing:
 figlet     x86_64     2.2.5-25.20151018gita565ae1.fc38        fedora     137 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 137 k
Installed size: 666 k
Downloading Packages:
figlet-2.2.5-25.20151018gita565ae1.fc38.x86_64. 1.2 MB/s | 137 kB     00:00
--------------------------------------------------------------------------------
Total                                           193 kB/s | 137 kB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1
  Installing       : figlet-2.2.5-25.20151018gita565ae1.fc38.x86_64         1/1
  Running scriptlet: figlet-2.2.5-25.20151018gita565ae1.fc38.x86_64         1/1
  Verifying        : figlet-2.2.5-25.20151018gita565ae1.fc38.x86_64         1/1

Installed:
  figlet-2.2.5-25.20151018gita565ae1.fc38.x86_64

Complete!
--> Pushing cache []:b5be31b75a7b031ee291e82907b39c9103ca848683d349aaef5c9e28ad94388b
--> 70ea8b96d07
STEP 3/4: ADD ./messagefile /messagefile
--> Pushing cache []:10ab90b4d35516f71a092ba0348367d3f0a1e5194fc36b5b321aeab8ba0202b0
--> 08d3196efe3
STEP 4/4: CMD cat /messagefile | figlet
COMMIT
--> Pushing cache []:08354a00bfa748c1dad8d8833f91c75f3a6ccefb370df730735711ecb461e1dd
--> 016f667375a
016f667375a74fb752d4f929f08b6b5a90ca319b178d4fca693fba152fde84e0
```
</details>

作成したコンテナイメージを確認します。
```
podman images
```

<details open>
<summary>実行例</summary>
  
```
$ podman images
REPOSITORY                         TAG         IMAGE ID      CREATED     SIZE
registry.fedoraproject.org/fedora  latest      c9bfca6d0ac2  3 days ago  196 MB
localhost/hw                       1.0         016f667375a7  6 days ago  437 MB
```
</details>

localhostにhwというコンテナが、TAG1.0で作成されているのを確認できました。

では、早速実行してみましょう。

```
podman run hw:1.0
```

<details>
<summary>実行例</summary>
  
```
$ podman run hw:1.0
 _   _      _ _        __        __         _       _
| | | | ___| | | ___   \ \      / /__  _ __| | ____| |
| |_| |/ _ \ | |/ _ \   \ \ /\ / / _ \| '__| |/ / _` |
|  _  |  __/ | | (_) |   \ V  V / (_) | |  |   < (_| |
|_| |_|\___|_|_|\___/     \_/\_/ \___/|_|  |_|\_\__,_|


```
</details>

Hello WorldのAAが表示されましたね。

ここで、各自5分～10分程度使って、以下のような内容を試してみましょう。
* messagefileの中身を好きな言葉にして再度ビルド・実行し、その結果を楽しみましょう
* REPO名をhelloworldではなく、他の好きな文字に変えて`podman images`の結果を確認してみましょう。実行してみましょう。
* TAGを1.0から1.1や1.2にして、`podman images`の結果を確認してみましょう。実行してみましょう。
* `podman ps -a`を実行すると、tag1.0などの古いコンテナが貯まっていますね。コンテナを削除してみましょう。イメージも削除してみましょう。
* ここまで激余裕という方は、FROMのfedoraをubuntuやbusyboxなどに変えて実行してみましょう(当然、figletの導入方法も変わりますよ)

dockerfileには多くのコマンドがあり、すべては紹介しきれません。より多くのコマンドを知りたい方は、以下をご確認ください。
* Dockerfileリファレンス(日本語翻訳版): https://docs.docker.jp/engine/reference/builder.html

 注) ContainerfileもDockerfileも、どっちも同じ構文です。
