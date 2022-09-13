<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# Install

## 1. install Packages from APT (Ubuntu)

JupyterHubにはコア部分としてPython、ネットワークでの公開にNode.jsが使われており、以下のものをインストールする。

- python3 (Python)
- pip (Python パッケージ管理ツール)
- nodejs (Node.js)
- npm (Node.js パッケージ管理ツール)

```
apt install node python3 pip npm
```

## 2-1. Install packages with pip

JupyterHubをインストールする。

以下の2つを`pip`を使ってインストールする。
- jupyterhub
- jupyterlab

`pip`はカレントユーザーのカレントディレクトリにインストールするローカルインストールとrootで全ユーザーに対してインストールするグローバルインストールがある。ここでは複数ユーザーに提供することを想定してグローバルインストールを行う。そのためroot出ない場合は`sudo`を付けることを忘れないでおきたい。

```
pip install jupyterhub jupyterlab
```

## 2-2. Install packages with npm

Node.jsのパッケージ管理ツール`npm`を使ってJupyterをブラウザ上で提供するためのパッケージをインストールする。

`npm`も同様に"-g"オプションでグローバルインストールになるため非rootユーザーであるならば`sudo`を付ける必要がある。

```
npm install -g configurable-http-proxy
```

---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
