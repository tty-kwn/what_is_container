# Containerfileを作ってみよう
## HelloWorld
任意のフォルダにContainerfileというファイルを作ります。
例えば、
```
mkdir ~/work/104
cd ~/work/104
echo "Hello World" > messagefile
vi Containerfile
```

Containerfileには、以下を記載します。
```
FROM ubuntu
RUN apt update && apt install figlet
ADD ./messagefile /messagefile
CMD cat /messagefile | figlet
```

Containerfileのコマンド説明は下記参照。

https://qiita.com/mintak21/items/a6766e3efd6730c9519d

DockerfileもContainerfileも同じ。「Podman」なので「Docker」fileではなく「Container」file。

ビルド実行
```
podman build .
```

TODO 出力結果
