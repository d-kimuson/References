## シェルスクリプトとは

- [初期設定](#chapter1)
- [スクリプトを書く](#chapter3)
- [スクリプトに実行権限を与える](#chapter4)
- [シェルスクリプトの文法](#chapter5)

<a id="chapter1"></a>

## 初期設定
### コマンドを設置するディレクトリを作成

``` sh
$ cd ~
$ mkdir Commnads
```

### パスを通す

パスを通すには, **~/.bashrc** を編集.

zshユーザーなら **~/.zshrc** .


一番下の行に，

``` sh
export PATH=~/Commnads:$PATH
```

と追記.

<a id="chapter2"></a>

## シェルスクリプトの記述法

``` sh
#!/bin/sh
```

を先頭に記述して, それ以降にUnixコマンドを羅列していく.


**例**

``` sh
#!/bin/sh

cd ~
touch hogehoge.txt
```

<a id="chapter3"></a>

## スクリプトに実行権限を与える

``` sh
chmod a+x hogehoge
```

で実行権限を付与.

<a id="chapter4"></a>

## シェルスクリプトの文法

- [コメントアウト](#grammar0)
- [変数](#grammar1)
- [入・出力](#grammar2)
- [算術計算](#grammar3)
- [IF文(条件分岐)](#grammar4)
- [FORループ](#grammar5)
- [WHILEループ](#grammar6)
- [関数](#grammar7)

<a id="grammer0"></a>

### コメントアウト

```sh
#!/bin/sh

# デスクトップディレクトリに移動
cd Desktop
```

<a id="grammar1"></a>

### 変数

スペースをあけずに変数=値.

変数にアクセスするには, *$変数名*

```sh
#!/bin/sh

VALUE=10
# 文字列はダブルクオーテーション(")で囲む
MESSAGE="代入してるYO"

echo $MESSAGE
```

**特殊な変数**

| 変数 | 値 |
| :---: | :---: |
| $0 | スクリプト名 |
| $1 | 第1引数 |
| $2 | 第2引数(以降も同様) |
| $# | 引数の数 |

コマンドの実行結果を変数に代入したければバッククォート(\`)で囲えばOK．

``` sh
#!/bin/sh

touch hogehoge.txt
PATH=`pwd`
echo $PATH"/hogehoge.txt"
echo "を生成(更新)しました！"
```

<a id="grammar2"></a>

### 入・出力

入力待ちは，
*read*
，出力は，
*echo*

``` sh
read NAME
echo -e "$NAMEさんが入力したゾ\nこんにちは！"
```

<a id="grammar3"></a>

### 算術計算

算術計算は，
``` sh
`expr 数値 オペランド 数値`
```

**オペランド一覧**

| オペランド | 意味 |
| :---: | :---: |
| + | 加算 |
| - | 減算 |
| \* | 乗算 |
| / | 除算 |
| % | 剰余算 |
| == | 等しい(真偽値を返す) |
| != | 等しくない(真偽値を返す) |

<a id="grammar4"></a>

### IF文(条件分岐)

<a id="grammar5"></a>

### FORループ

<a id="grammar6"></a>

### WHILEループ

<a id="grammar7"></a>

### 関数
