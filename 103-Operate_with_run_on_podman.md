
ターミナル[1]で以下を実行
```
podman run -it ubuntu bash
```

別のターミナル「ターミナル[2]」で実行
```
podman run -it --name fedora-t2 fedoraos bash
```

さらに別のターミナル「ターミナル[3]」で実行
```
podman ps
```

ターミナル[1]で実行していたubuntu bashでexitし、ターミナル[3]でもう一度
```
podman ps
```
を実施、ubuntuが消えていることを確認。

ターミナル[1]で以下を実行し、bashが起動することを確認。
```
podman exec -it fedora-t2 bash
