<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# Manual JupyterHub

## About

Jupyter NotebookはPCのローカルにWebサーバーを立てそこにブラウザでアクセスできるようにしたいわばWebページである。
この計算をするのはWebサーバー側であるがローカルにJupyter Notebook環境を立てたことにより計算能力は今使っているPCのスペックに依る。
したがって当然、他のマシンにJupyter Notebook環境立てて、自分のPCからはブラウザを通したアクセスだけ、計算はサーバーにやらせるといった使い方が期待される。

Jupyter HubはJupyter Notebookをサーバーサイドに設置できるようにしてマルチユーザーアクセスに対応したものである。

## Index

- [インストール](./docs/installing.md)

- [JupyterHubの設定](./docs/setting_item.md)

- [JupyterHubの自動起動](./docs/jupyterhub_service.md)

<!-- Written by Croyfet in 2022-->
