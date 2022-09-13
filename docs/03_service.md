<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# Service

JupyterHubは常駐させて、バックグラウンドで動くことが望ましい。
また起動時には自動で起動するようになっていると便利であるためJupyerHubをサービスとして登録する。

## .service

Serviceは.serviceに書かれた内容を起動時や実行時に読み込む。
.serviceファイルの実態は大体"/etc/systemd/system"に置き、それをコマンドでシンボリックリンクを貼り、読み込む。

.serviceの内容は詳しくは言及しないがサンプルを示す。

[Sample (jupyterhub.service)](../template/jupyterhub.service)

JupyterHubのconfigなどを変えた場合は随時変更する。

## サービス化

先のserviceファイルを有効化するために`systemctl`コマンドを使い

```
systemctl enable jupyterhub.service
```
を実行する。

以下のコマンドでステータスを確認できるし
```
systemctl status jupyterhub
```

`start`で手動で起動できる。
```
systemctl status jupyterhub
```

---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
