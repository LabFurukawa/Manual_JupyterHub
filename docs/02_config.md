<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# Setup JupyterHub config

## JupyterHubの実行

JupyterHubを実行する場合

```
jupyerhub _CONFIG_FILE_PY_
```

で実行する。

```
jupyterhub
```
でも実行はできるがconfigファイルが読み込まれず既定の設定で開始するため、使わない。

またうまく実行できなかった場合やconfigの読み込みを忘れた場合、その実行したディレクトリにログやキャッシュファイルのようなものが生成されるので違う設定で再び起動したい場合は削除する。

## JupyterHubのconfigの作成方法

下記のコマンドでconfigファイルを作成できる。

場所としては`/etc/jupyterhub`ぐらいが無難だろう。

```
jupyterhub --generate-config
```

しかし冗長なので最低限のサンプルを提示する。

[Sample (jupyterhub_config.py)](../template/jupyterhub_config.py)

## jupyterhub_config.py リファレンス

### IP/port

- `c.JupyterHub.ip`

	JupyterHubを公開するIPアドレスでありインストールしているマシンのIPアドレス

	`ifconfig`コマンド等で確認できる。言うまでもないがDHCPは無効にして手動でIPを割り振らないと計算機の再起動のたびにIPアドレスが変わるためアクセスできなくなる。

	```
	c.JupyterHub.ip = 'xx.xx.xx.xx'
	```

- `c.JupyterHub.port`

	ポートは一般的にHTTPは80番が使われる。他の番号を使った場合、例えば"yy"ポートを使うときブラウザからアクセスするときに"xx.xx.xx.xx:yy"と打ち込む必要があり見栄えが悪い。80番は省略することができる。

	```
	c.JupyterHub.port = 80
	```

### User

- `c.Authenticator.admin_users`

	WebUIからシャットダウンなどの操作ができる管理者ユーザーの登録。ここに登録されたユーザーは次の`c.Authenticator.allowed_users`に自動で追加される。

	```
	c.Authenticator.allowed_users = {'user_admin'}
	```

- `c.Authenticator.allowed_users`

	JupyterHubを使用できるユーザーの登録

	```
	c.Authenticator.allowed_users = {'user_01', 'user_02', 'user_03'}
	```

### Spawner

- `c.Spawner.notebook_dir`

	JupyterNotebookで生成するドキュメントのディレクトリを指定する。
	それぞれのユーザーディレクトリに生成されるよう"~/"で指定するのが妥当

	ちなみにこの指定したディレクトリが存在しない場合Webからのアクセスが失敗する。

	ここでは"~/JupyterHubRoot"ぐらいにしておく。

	```
	c.Spawner.notebook_dir = '~/JupyterHubRoot'
	```


## JupyterHubの実行確認

jupyterhubのconfigの置いたディレクトリに移動し、serviceとしてrootで実行することを想定し以下のように実行する。

in /etc/jupyterhub
```
sudo jupyterhub jupyterhub_config.py
```

これで指定のアドレス、ポートからアクセスできたら成功である。

ちなみにローカルマシンで実行するJupyterNotebookは`jupyter notebook`コマンドで勝手に立ち上がっているが、それはJupyterNotebookが起動し、そのURLをブラウザで開いているだけでアプリがそのもの立ち上がっているわけではない。本質はJupyerNotebookがHTTPで動くことであり、ブラウザが立ち上がることではない。
当然、`jupyterhub`コマンドを実行してもブラウザは立ち上がらない。URLを叩いて自分でアクセスし、次回からはアクセスしやすいようブックマークをしておくといいだろう。

---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
