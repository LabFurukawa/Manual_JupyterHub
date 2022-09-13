<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->


# Activate Julia

JuliaをJupyterHubで使う。

## Install

普通は"/opt"にインストールする。

### 1. Download

`wget`でjuliaを取ってくる。URLはwebページから拾ってくる。
ここではLTSのv1.6.7をダウンロードする。

```
wget https://julialang-s3.julialang.org/bin/linux/x64/1.6/julia-1.6.7-linux-x86_64.tar.gz
```


### 2. Unzip
tar.gzなので解凍

```
tar -zxvf julia-1.6.7-linux-x86_64.tar.gz
```

### 3. link

無難に様々なバージョンに対応できるようシンボリックリンクを張る。

```
ln -s julia-1.6.7 julia
```

### 4. PATH

一部ユーザーだけなら"~/.bashrc"から読み込まれる"~/.bash_aliases"に記述するのが一般的だが
今回は全ユーザーに読み込ませることを考えて"/etc/profile"から読み込まれる"/etc/profile.d/*.sh"にPATHを記述する。

以下のファイル"/etc/profile.d/julia.shを作成して
```
export PATH=$PATH:/opt/julia/bin
```
と記述する。

```
source /etc/profile
```
でリロードをかける。
```
echo $PATH
```
でPATHが通っているか確認することもできるし
```
julia -v
```
でバージョンが表示されるか確認するのもよい。

## IJulia

Jupyter環境でJuliaを実行するためのパッケージをJulia内のパッケージ管理ツールPkgから追加する。

### Juliaの起動

```
julia
```

閉じるときは'Ctrl'+'D'か
```
julia> exit()
```
で閉じることができる。

### Pkgを開く
パッケージ管理ツールはjuliaから

```
julia>]
```
で切り替わり
```
(@v1.6) pkg>
```
となる。ここでBackSpaceを押せば元のJuliaに戻れる。

### IJuliaのインストール

Pkgで

```
add IJulia
```
でダウンロードできる。
これによりローカルインストールが行われ"~/.local/share/jupyter/kernels/julia-1.6"にconfigが追加される。

そのためユーザー毎にこの動作を行う必要がある。

## 並列実行

Juliaはデフォルトでは1スレッド動作をする。

```
julia> Threads.nthreads() 
```
と実行することでスレッド数が取得できるはずである。

マルチスレッドで実行するためにはコンソールからの場合"-t"または"--threads"でスレッド数を指定する。
2スレッドで実行するとき
```
julia -t 2
```
で実行すれば2スレッドで実行できる。

他に環境変数に"JULIA_NUM_THREADS=2"を追加するという手段がある。
先の/etc/profile.d/julia.shあたりに以下のように追加する。

```
export JULIA_NUM_THREADS=2
```

`source`コマンドでリロードは忘れない。

ただし、この環境変数はJupyterHub(IJulia)からは参照されない。JupyterHubから`Julia`でマルチスレッドを利用するには先のIJuliaをインストールしたときに"~/.local/share/jupyter/kernels/julia-1.6"に追加された"kernel.json"内にある`env`を編集して

```
"env": {"JULIA_NUM_THREADS": "2"}
```
のように指定する。


---
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
