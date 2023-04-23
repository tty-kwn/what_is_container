# dotnet SDKのインストール
こちらから、プラットフォームにそってインストールを行ってください。
https://dotnet.microsoft.com/ja-jp/download/dotnet?cid=getdotnetcorecli

私は、このmd作成時点で長期サポートでGAしていたバージョン6の「アプリのビルド」>「SDK 6.0.408」>「Windows」>「x64」からダウンロードしインストールしています。

```
cd ~/work
dotnet new webapp --name firstdotnet
```

<details>
<summary>実行例</summary>

```
$ dotnet new webapp --name firstdotnet

.NET 6.0 へようこそ!
---------------------
SDK バージョン: 6.0.408

テレメトリ
---------
.NET ツールは、エクスペリエンスの向上のために利用状況データを収集します。データは Microsoft によって収集され、コミュニティと共有されます。テレメトリをオプトアウトするには、好みのシェルを使用して、DOTNET_CLI_TELEMETRY_OPTOUT 環境変数を '1' または 'true' に設定できます。

.NET CLI ツールのテレメトリの詳細をご覧ください: https://aka.ms/dotnet-cli-telemetry

----------------
ASP.NET Core の HTTPS 開発証明書をインストールしました。
証明書を信頼するには、'dotnet dev-certs https --trust' (Windows および macOS のみ) を実行します。
HTTPS の詳細については、https://aka.ms/dotnet-https を参照してください
----------------
最初のアプリを作成するには、https://aka.ms/dotnet-hello-world を参照してください
最新情報については、https://aka.ms/dotnet-whats-new を参照してください
ドキュメントを探索するには、https://aka.ms/dotnet-docs を参照してください
GitHub で問題の報告とソースの検索を行うには、https://github.com/dotnet/core を参照してください
'dotnet --help' を使用して使用可能なコマンドを確認するか、https://aka.ms/dotnet-cli にアクセスしてください
--------------------------------------------------------------------------------------
テンプレート "ASP.NET Core Web App" が正常に作成されました。
このテンプレートには、Microsoft 以外のパーティのテクノロジが含まれています。詳しくは、https://aka.ms/aspnetcore/6.0-third-party-notices をご覧ください。

作成後の操作を処理しています...
.\firstdotnet\firstdotnet.csproj で ' dotnet restore ' を実行しています...
  復元対象のプロジェクトを決定しています...
  .\firstdotnet\firstdotnet.csproj を復元しました (111 ms)。
正常に復元されました。
```
</details>

```
dotnet build
```

<details>
<summary>実行例</summary>
  
```
$ dotnet build
MSBuild version 17.3.2+561848881 for .NET
  復元対象のプロジェクトを決定しています...
  復元対象のすべてのプロジェクトは最新です。
  firstdotnet -> ...\firstdotnet\bin\Debug\net6.0\firstdotnet.dll

ビルドに成功しました。
    0 個の警告
    0 エラー

経過時間 00:00:08.53
```
</details>

```
dotnet run
```

<details open>
<summary>実行例</summary>
  
```
$ dotnet run
ビルドしています...
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: https://localhost:7297
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5146
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: ...\firstdotnet\
```
</details>

実行例にある通り、ブラウザでhttp://localhost:5146 にアクセスします。(ポート番号は環境によってランダムなので、実行時の情報を必ず確認してください)<br/>
Webアプリが実行されていることが確認できました。

Ctrl+Cでストップします。

TODO: [ここ](https://learn.microsoft.com/ja-jp/aspnet/core/host-and-deploy/docker/building-net-docker-images?view=aspnetcore-6.0)を読み解いて、続きを実施する
