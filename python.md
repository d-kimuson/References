# Python3 文法メモ

## 目次

### 基本編
- [Python環境構築](#chapter0)
- [Pythonの特徴(多言語との違い)](#chapter1)
- [コメントアウト](#chapter2)
- [変数](#chapter3)
- [主要な型(タイプ)](#chapter4)
    1. [文字列( str型 )](#chapter4-1)
    1. [型の確認](#chapter4-2)
    1. [キャスト(型変換)](#chapter4-3)
- [演算子](#chapter5)
    1. [is と == の違い](#chapter5-1)
- [関数](#chapter6)
    1. [関数の定義](#chapter6-1)
    1. [関数の呼び出し](#chapter6-2)
    1. [デフォルト引数](#chapter6-3)
    1. [print関数](#chapter6-4)
- [クラス](#chapter7)
    1. [クラスの定義](#chapter7-1)
    1. [インスタンス生成](#chapter7-2)
- [リスト](#chapter8)
- [シーケンス型](#chapter9)
    1. [タプル](#chapter9-1)
    1. [文字列](#chapter9-2)
    1. [range](#chapter9-3)
- [ディクショナリ](#chapter10)
    1. [キーとバリューのリストを取得](#chapter10-1)
    1. [値の追加と削除](#chapter10-2)
- [for文](#chapter11)
    1. [多言語っぽいforループ](#chapter11-1)
    1. [リストを使ったforループ](#chapter11-2)
    1. [ディクショナリを使ったforループ](#chapter11-3)
- [if-elif-else文](#chapter12)
- [while文](#chapter13)
- [モジュールのインポート](#chapter14)
    1. [import モジュール](#chapter14-1)
    1. [from モジュール import クラス](#chapter14-2)
    1. [import モジュール as エイリアス](#chapter14-3)
    1. [自作モジュールのインポート](#chapter14-4)
- [例外処理](#chapter15)


### 応用編
- [f-strings 記法](#application1)
- [関数における5種類の引数](#application2)
- [スライス](#application3)
- [リストの内包表記](#application4)
- [自作モジュールについて](#application5)
- [スクレイピング](#application6)
- [正規表現](#application7)
- [プログラム中からUnixコマンドの実行](#application8)
- [グラフ描写](#application9)
- [仮想環境構築](#application10)


### 基本的なモジュール

- [re](#module_re)
- [sys](#module_sys)
- [time](#module_time)
- [subprocess](#module_subprocess)
- [pandas](#module_pandas)
- [matplotlib](#module_matplotlib)
- [requests](#module_requests)


<a id="chapter0"></a>

## Python環境構築

Pythonはもうほぼ3系に移行してて個人レベルでは2系を使うことはほぼほぼないんだけど, 割と最新のPython3だと動かなくてちょっと古いPython3を使いたいみたいなことはあるのでバージョンを管理(切り替え)できるようなツールが必要.

でバージョン管理のやり方は,

1. virtuarenv(venv)
2. Pyenv
3. Anaconda ディストリビューション

を使う方法がある.

Anacondaは強いんだけど, なんか独自の手法でパス管理をしてるらしくてzsh使ってるとコマンド見つかんねえよって怒られることがあったり, あと標準とは違うパスにPythonが設置されるからツールの初期設定とかがめんどくなることが間々ある.

ただ, 一応venvやpyenvっぽいこともcondaでできるから多機能なのは間違いないけど, 記事とかで使ってる情報ソースがやっぱvenvばっかだし, わざわざconda使うか?って感じ. いろんなモジュール最初からあるのも便利っちゃ便利だけどpip最強だから正直そこまで恩恵が()

Pyenvは, Python自体のバージョン管理に特化してて, venvはモジュールのバージョン管理もできる. venvかcondaは結構必須な感じする. 正直, Python自体のバージョン管理専用のコマンドを別に用意する必要性が薄く感じるからvenvでいいかな感.

venvは, PyenvやAnacondaと違ってツールの上にPythonをインストールするんじゃなくて標準のPythonを補強する感じのツールだからありがたみが深み.

てことで, シンプルなPython + virtualenvの環境構築をする.

``` sh
brew install python3
```

pythonの実行で, いちいちpython3と書くのはめんどいからエイリアスを設定する

``` sh
alias python=python3
alias pip=pip3
```

と, *.bash_profile* に記述することでpythonとpipでそれぞれ3系のpythonとpipを利用できるようになる(有効にするにはターミナルを再起動).

pipは最強だからなんかモジュールみつからんて言われたら **pip install <モジュール名>** てコマンド打っとけば勝手にインストールしてくれる.

手始めに, pipでvirtualenbvを導入する.

``` sh
pip install virtuarenv
```



<a id="chapter1"></a>

## Pythonの特徴(多言語との違い)
- コンパイルなしで実行
- 平易で可読性の高い文法
- あらゆる値がオブジェクト
- ブロックの区切り( Cでいう{} )はインデントで
-  モジュール(ライブラリ)の暴力で，大体のことはなんでもできる
- 工夫しないと遅い(らしい)けど，これもモジュールの暴力でなんとかなる

<a id="chapter2"></a>

## コメントアウト

\# から改行まではコメントになる

``` Python
x = 10 # ここはコメント
y = 12 # yに12を代入！
```

<a id="chapter3"></a>

## 変数

- 変数の宣言は不要( 直接呼び出して代入すればいい )
- (明示してないだけってことじゃなく)変数自体に型の概念なし
- 数値いれといた変数に文字列入れ直すとかもできちゃう

``` Python
x = 10 # 宣言が無いので，即変数に代入
print( x )
x = "Koshikawa" # 変数自体には型がないので，同じ変数にまた別の型をいれ直すことも
print( x + "さんこんにちは！" )
```

<a id="chapter4"></a>

## 主要な型(タイプ)

無数の型があるけど主要なのは，

| 型(タイプ) | 意味 |
| :---: | :--- |
| int | 整数 |
| float | 少数 |
| str | 文字列 |
| bool | 真偽値( True/False ) |
| None | null的なモノ |

<a id="chapter4-1"></a>

### 1. 文字列( str型 )
文字列は，

- シングルクォーテーション(')
- ダブルクオーテーション(")
- トリプルクォーテーション('''または""")

のいずれかで囲む．

トリプルクォーテーションは複数行の文字列で，改行を反映してくれる．

``` Python
value = 'abc'
name = "Koshikawa"
message = """こんにちは！
はじめまして！
やっほー！"""
```

Pythonでは，あらゆる値はオブジェクトでそれぞれのタイプ(クラス)に定義された独自のメソッドを使える．文字列( str型 )も例外ではない．

``` Python
name = "Koshikawa".replace( "sh", "s" ) # 置換
year, month, day = "2018,10,11".split( "," ) # 分割
```

などなど．

より高度な
[f-strings記法](#application1)
もある．

<a id="chapter4-2"></a>

### 2. 型の確認
type関数で行う

``` Python
type( "我が名は越川なり！" ) # str を返す
```

<a id="chapter4-3"></a>

### 3. キャスト(型変換)

キャストは，型名()でする

``` Python
name = "Koshikawa"
age = 15

# ageは int型なので str型にキャストしないと連結できない
print( name + "さんの年齢は，" + str(age) + "歳です．" )
```

<a id="chapter5"></a>

## 演算子

- 四則演算子と比較演算子は一般的なモノと同じ
- 累乗を ** 演算子で計算できる
- 小数点以下切り捨ての除算を // 演算子で計算できる
- インクリメント( i++とか )，デクリメント( i-- )は無し => 代わりに i += 1とかを使う．

| オペランド | 意味 | 例 |
| :---: | :--- | :---: |
| + | 数値なら加算，文字列なら連結 | 10 + 20 |
| - | 減算 | - |
| * | 数値なら乗算，文字列なら繰り返し | - |
| ** | 累乗( x^y ) | - |
| / | 除算( 小数点以下そのまま ) | - |
| // | 除算( 小数点以下切り捨て ) | - |
| % | 剰余算 | - |
| = | 代入 | x = 3 |
| == | 等しい(等価)( True/Falseを返す ) | x == 10 |
| != | 異なる( True/Falseを返す ) | - |
| > | より大きい( True/Falseを返す ) | - |
| >= | 以上( True/Falseを返す ) | - |
| < | より小さい( True/Falseを返す ) | - |
| <= | 以下( True/Falseを返す ) | - |
| and | 論理積( True/Falseを返す ) | x > 3 and y < 5 |
| or | 論理和( True/Falseを返す ) | - |
| not | 論理否定( True/Falseを返す ) | not x <= 10 |
| is | 等しい(同一)( True/Falseを返す ) | x is y |
| in | 含むかどうかの判定( True/Falseを返す ) | "s" in "Koshikawa" |

<a id="chapter5-1"></a>

### 1. is と == の違い

- == は等しい値かどうかを判定
- is は同じインスタンスかを判定
- isのが速い

isのが速いけど，同一インスタンスかをみてる

値が等しいかをみたいことがほとんどだから基本 ==

一般的なisの用途は，**型の比較** のみ

Noneとかstrとかは **プログラム中に一つしか存在しないインスタンス** だから，type()の返り値とか使って型比較をするならisでOK．しかも==より高速！


``` python
name = "Koshikawa"
obj = None

if type( name ) is str:
    print( name + "さんこんにちは！" )

if obj is None:
    print( "Noneだぞ" )
```

[参考サイト](https://www.python-izm.com/tips/difference_eq_is/)

<a id="chapter6"></a>

## 関数

とりあ，メソッドと関数があるけど，

- クラス内に定義された関数を *メソッド*
- そうでないやつを *関数*

と呼ぶこととしておく．んで，この章は関数について．

<a id="chapter6-1"></a>

### 1. 関数の定義

- 関数はdefで定義する
- Cみたいなプロトタイプ宣言は必要ない
- 必要な引数はカンマ区切りで羅列

**基本的な形**

``` python
def hello_message(name):
    message = name + "さん，さあ一緒にhelloworld!!"
    return message
```

引数がない関数にしたいなら引数無しで定義すれば良いし，返り値をなしで設計したければreturn文を書かなければ良いだけ．

<a id="chapter6-2"></a>

### 2. 関数の呼び出し

普通に呼ぶだけ．

``` Python
message = hello_message( "Koshikawa" )
print( message )
```

<a id="chapter6-3"></a>

### 3. デフォルト引数

Pythonには，Javaで言うオーバーライドだかオーバーロードだかがない代わりにデフォルト引数( 引数が与えられなかったときにデフォルト値を渡す )がある．これで，与えれた引数次第で処理を変えるように記述すればオーバーロード？ライド？と同じような効果が期待できる．

``` Python
def hello( name="Koshikawa" ):
    print( name + "さんこんちゃす" )

hello() # Koshikawaさんこんちゃす
hello("Tarou") # Tarouさんこんちゃす
```

この他にも，
[関数の引数には種類]()
がある．

<a id="chapter6-4"></a>

### 4. print関数

print関数には，end引数があって文末を選べるけど，普段はデフォルト引数で改行になってるっぽいから，普通に使うと勝手に改行される．したくないprintは，

``` Python
print( "名前: ", end="" )
print( "こしかわ" )
# 名前: こしかわ
# と表示される！
```

みたいにすればおけ．

<a id="chapter7"></a>

## クラス

クラス(雛形) => インスタンス(実物)を生成

- **インスタンス.変数** で 変数にアクセス
- **インスタンス.メソッド()** で メソッドを使える

<a id="chapter7-1"></a>

### 1. クラス定義

- クラス定義は class で行う
- 自身のインスタンスを指す **self** がキーワード
- メソッドの引数には必ず **self** ( 自身のインスタンス )を渡す
- **self.変数** で 自身のパラメータ( 変数 )にアクセス
- コンストラクタは， \_\_init\_\_( self, ... )メソッド

``` Python
class Fuman:
    name = "Taro" # パラメータ

    def __init__( self, name ): # コンストラクタ
        self.name = name # インスタンスのname変数に，引数のnameを代入
    def printName( self ):
        print( "名前: " + self.name )
```


<a id="chapter7-2"></a>

### 2. インスタンス生成

- クラス名()でインスタンス生成をする．
- コンストラクタに渡したい引数は，生成時に関数の引数みたいに渡す．

``` Python
Koshi = Fuman( "Koshikawa" )
Koshi.printName() # 名前: Koshikawa
```

<a id="chapter8"></a>

## リスト

- 多言語での *配列* の型制限がない版(一つのリストに複数の型が混在できる)
- []に カンマ( , ) 区切りで入力する．
- 配列みたいに リスト[index]で要素にアクセス

``` Python
koshikawa_list = [ "Koshikawa", 20, "1999年1月1日", "s1250134" ]
print( koshikawa_list[0] + "さんは" + str( koshikawa_list[1] ) + "歳です" )
```

**要素の追加** は，

- リスト.append( value )
- リスト.insert( 挿入インデックス, value )

で行う．

普通に後ろに追加するだけならappendで，場所選んで追加したいならinsert使えばおけ．

ちな，範囲外のインデックス指定して無理やり代入して追加するのは不可能.

index out of rangeみたいなError吐かれる．

``` Python
sample_list = [0, 1, 2]
sample_list[3] = 3 # index out of range error
```

**要素の削除** は，

- リスト.pop()
- リスト.pop( 削除インデックス )

で行う．

popメソッドの削除インデックスを指定するデフォルト引数は末尾になってるから，後ろから１個削除したいだけなら引数なし．

指定したとこから削除したいならインデックスを渡す．

リストは割と奥が深くて

- [スライス]()
- [リストの内包表記]()

などの使い方もある．

<a id="chapter9"></a>

## シーケンス型

シーケンス型はリストっぽいもの全般を指す言葉．

リストも含めて，複数の値を **順番に** 羅列したもの．

- リスト
- タプル
- 文字列
- range
- その他リストライクなもの

などがあって，list関数でリストにキャストできる．

listっぽいけど，実はlistじゃないから不都合ってことが時折あって，list以外のシーケンス型 => list型への変換は結構する．

<a id="chapter9-1"></a>

### 1. タプル

- リストの定数版，値が変更できない
- ()で囲んで，カンマ( , )区切り
- リストでよくね感やばい

<a id="chapter9-2"></a>

### 2. 文字列

文字列も文字の羅列だからこれにあたって結構リストとの親和性が高い．

``` Python
name = "Koshikawa"
listed_name = list( name ) # ['K', 'o', 's', 'h', 'i', 'k', 'a', 'w', 'a']
```

<a id="chapter9-3"></a>

### 3. range

range関数っていうのがあって，for文と合わせてよく使う．

- 開始( デフォルトで0 )
- 終了
- 間隔( デフォルトで1 )

の３種類の引数で，数字の羅列を作ってくれる．

``` Python
range1 = range( 5 ) # [0, 1, 2, 3, 4]
range2 = range( 1, 5 ) # [1, 2, 3, 4]
range3 = range( 1, 5, 2 ) # [1, 3]
```

ただ，print(range1) しても range(0, 5)としか返してくれないから中身みたければ，list でキャストすれ必要あり．

<a id="chapter9-4"></a>

### 4. reversed()関数

reversed関数は，

- シーケンス型の逆順を作ってくれる関数
- range関数とセットで使うか，文字列の逆順取得とかで使う
- rangeはforループとセットで使うのが主な用途だけど，デクリメント系の回し方が非直感的(ずらしが必要)だからこいつの助けを借りる
- 生成されるのは list_reverseiterator( イテレータはリストではない )
- リストとして使いたいならキャストが必要

``` Python
# 5, 4, 3, 2, 1, 0 を作りたい!!

# 直感的ではないけど，rangeから作る
sample2 = range(5, -1, -1)

# reversed( range( ... ) ) で作る
sample1 = reversed( range( 6 ) )
```

<a id="chapter10"></a>

## ディクショナリ

- リストの数値ではなく，キーワードで要素にアクセスする版的な
- key( リストで言うインデックス ) と value( 要素 ) から成る
- 順番はないので シーケンス型ではない(マップ型とか言うらしいけどよく知らない)
- key : value と対を書き，カンマ( , )で区切って，{}で囲む

``` Python
koshikawa_data = { # 1行に書いてもおけ
    "name": "Koshikawa",
    "age" : 20,
    "id": "s1250133",
    "自己紹介": "スカイズに栄光あれ！"
}

print( koshikawa_data["name"] + "さんおはよう世界" )
```

<a id="chapter10-1"></a>

### 1. キーとバリューのリストを取得

keys()メソッド とvalues()メソッド で，keyの一覧とvalueの一覧をそれぞれシーケンス型で取得できる．

``` python
keys = koshikawa_data.keys() # dict_keys(['name', 'age', 'id', '自己紹介'])
values = koshikawa_data.values() # dict_values(['Koshikawa', 20, 's1250133', 'スカイズに栄光あれ！'])

# dict_keysはリストライクだけどリストじゃなくて不都合 => キャストすると利用が楽
keys = list( keys ) # ['name', 'age', 'id', '自己紹介']
```

<a id="chapter10-2"></a>

### 2. 値の追加と削除

- 値の追加は，存在しないキーを指定して普通に代入すればおけ．
- 値の削除は，**pop( key )** メソッド ( 返り値は削除したバリュー )

``` Python
dict1 = {
    "one" : 1,
    "two" : 2,
    "three" : 3,
}

# key : "four", value : 4 組の追加
dict1[ "four" ] = 4

# key : "three", value : 3 組の削除( 取り出し )
poped_value = dict1.pop( "three" )

## 結果
## dict1.keys() = [ "one", "two", "four" ]
## poped_value = 4
```

<a id="chapter11"></a>

## for文

- 基本は，
``` Python
for <変数> in <シーケンス型>:
    <変数>に関する処理 ...
```
て感じ
- リスト(かリストライクなもの)を用意してあげて，リストの中身を順番に変数に渡して上げるっていうアルゴリズムで動いてる．

<a id="chapter11-1"></a>

### 1. 多言語っぽいforループ

は，
[range関数](#chapter9-3)
で実装する．

``` python
for i in range(5):
    print( i, end=", " )
print()
# 0, 1, 2, 3, 4
```

こんな感じ．

<a id="chapter11-2"></a>

### 2. リストを使ったforループ

リストの中身を順番に取り出していくループ．

``` Python
names = ["tarou", "sora", "jiro", "koshikawa"]
for name in names:
    print( name )
```

結構便利．

<a id="chapter11-3"></a>

### 3. ディクショナリを使ったforループ

前述のように，keys()メソッドでキーをシーケンス型で取得できるので，これを使う．

``` Python
for token in koshikawa_data.keys():
    print( token )
```

<a id="chapter12"></a>

## if-elif-else文

基本形は，

``` Python
if True:
    print( "checked if" )
elif True:
    print( "checked elif" )
else :
    print( "checked else" )
```

特に書くことないけど，
条件式は真偽値じゃなくても良くて，(たぶん)bool型にキャストしてみてくれるから便利

| 型 | False |
| :---: | :---: |
| int | 0 |
| str | 空文字( "" ) |
| list | 空リスト( [] ) |

FalseじゃなければTrueになる( 当たり前 )

``` Python
def introduction( intro="" ):
    if intro: # 引数の自己紹介文が表示
        print( intro )
    else : # デフォルト引数ならここを通る
        print( "自己紹介がないよ" )
```

こんな感じでデフォルト引数と合わせると便利．

<a id="chapter13"></a>

## while文

while文の基本形．

``` python
while( True ):
    if True:
        break
    elif True:
        continue
```

特に書くことない．

<a id="chapter14"></a>

## モジュールのインポート

主に３つの方法がある．

1. import モジュール
1. from モジュール import クラス
1. import モジュール as エイリアス

<a id="chapter14-1"></a>

### 1. import モジュール

``` Python
import sample_module

sample_class_instance = sample_module.sample_class()
```

ただこれだと長い．

sample_class使うときにsample_module.sample_class()て書くのは非生産的．

<a id="chapter14-2"></a>

### 2. from モジュール import クラス

``` Python
from sample_module import sample_class

sample_class_instance = sample_class()
```

<モジュール>から<クラス>をインポートするって書き方．これなら長くなくて良き．

<a id="chapter14-3"></a>

### 3. import モジュール as エイリアス

モジュール名に短いエイリアス(ニックネーム)を付けるというやり方．サンプルコードとかだと，この手法が一番多い気がする．

``` Python
import sample_module as sm

sample_class_instance = sm.sample_class()
```

<a id="chapter14-4"></a>

### 4. 自作モジュールのインポート

自作モジュールを他の.pyファイルで利用するにはパスを設定する必要がある.

Bash利用者なら **~/.bash_profile** , Zsh利用者なら **~/.zshrc** 辺りに,

``` sh
PYTHONPATH=<設定したいパス>:$PYTHONPATH
export PYTHONPATH
```

を記述すると, モジュールがおいてあるパスとして認識してくれる

また, 自作モジュールをインポートしたい.pyファイル内で,

``` Python
import sys
sys.path.append("<使用したい.pyが置かれてるディレクトリ>")
import hoge
```

のようにすることでもインポートができる.

高頻度に使うようなものなら前者の方法を, めったに使わないなら後者の方法で十分.

<a id="chapter15"></a>

## 例外処理

例外処理は try-except-else-finally文で行う

| 文 | 用途 |
| :---: | :--- |
| try | 例外が起こりうる処理 |
| except | 例外が起きたときの処理 |
| else | 例外が起きなかったときの処理 |
| finally | (例外の有無に関わらず)最後に実行する処理 |

except節では，

- 例外オブジェクトを渡す(渡した例外を取得する)
- 連ねて複数の例外オブジェクトをキャッチも可
- 渡さなければあらゆる例外をキャッチ(バグの温床になるため非推奨)
- Exception は 基底クラスで，上同様あらゆる例外をキャッチできる( 同様に非推奨 )

``` Python
def divide( x, y ):
try :
    print( str(x) + " / " + str(y) + " = " + str( x / y ) )
except ZeroDivisionError as e1:
    print( e1 )
except TypeError as e2:
    print( e2 )
else :
    print( "正常実行されました！" )
finally :
    print( "divideの終了\n" )

# deivideの実行
print( "divide(2, 3)の実行" )
divide( 2, 3 )
print( "divide(\"2\", \"3\")の実行" )
divide( "2", "3" )
print( "divide(4, 0)の実行" )
divide( 4, 0 )
```

で，実行結果が，

``` sh
divide(2, 3)の実行
2 ÷ 3 = 0.6666666666666666
正常実行されました！
divideの終了

divide("2", "3")の実行
unsupported operand type(s) for /: 'str' and 'str'
divideの終了

divide(4, 0)の実行
division by zero
divideの終了
```

例外があってもスルーしたいときはpass文

``` Python
try :
    print( 4 / 0 )
except : # あらゆる例外をキャッチ
    pass
```

<a id="application1"></a>

## f-strings 記法

より高度に文字列を扱う記法．

- 文字列の前に f を付けると，f-strings記法になる( f"hogehoge" )
- 変数を渡し，書式設定に応じた文字列にできる
- {}が置換フィールドで，この中にいろいろ書く
- {変数名:書式設定}みたいな感じ

例えば，

``` Python
name = "Koshikawa"
print( f"{name}さんこんにちは！" ) # Koshikawaさんこんにちは
```

### 書式まとめ

\:以降，以下の書式にしたがって記述すればおけ．

| 用途 | 1文字目 | 2文字目 | 3文字目 |
| :---: | :---: | :---: | :---: |
| 文字埋め | 埋めたい文字 |>(左), ^(中央), <(右) | 埋める数 |
| 0埋め | 0 | 埋める数 |  |
| 桁揃え | . | 揃えたい桁数 | g |
| 小数点以下の桁揃え | . | 揃えたい桁数 | f |
| 指数表記 | . | 揃えたい桁数 | e |
|割合表記 | . | 揃えたい桁数 | % |
| 2進数表記① | b |  |  |
| 8進数表記① | o |  |  |
| 16進数表記① | x |  |  |
| 2進数表記② | #b |  |  |

``` Python
name = "Koshikawa"
num = 8
floatnum = 1.2519471749817471974917
print( f"{name: <20}さんこんにちは！" )
print( f"{name: ^20}さんこんにちは！" )
print( f"{name: >20}さんこんにちは！" )
print( f"{num:05}" )
print( f"{num:.5g}" )
print( f"{floatnum:.5f}" )
print( f"{num:.2e}" )
print( f"{floatnum:.2%}" )
print( f"{num:b}" )
print( f"{num:#b}" )
```

で出力が，

``` sh
Koshikawa           さんこんにちは！
     Koshikawa      さんこんにちは！
           Koshikawaさんこんにちは！
00008
8
1.25195
8.00e+00
125.19%
1000
0b1000
```

<a id="application2"></a>

## 関数における5種類の引数

<a id="application3"></a>

## スライス

<a id="application4"></a>

## リストの内包表記

<a id="application5"></a>

## 自作モジュールについて

モジュールとして使用したいファイルが,
Users/User1/MyModule/sample.py
にあるとして,

``` Python
import sys
sys.path.append("Users/User1/MyModule")
import sample

sample.hogehoge()
```

でおけ.

<a id="application6"></a>

## スクレイピング

- requests
- BeautifulSoup

を使う.

``` Python
import requests
from bs4 import BeautifulSoup

url = "https://hogehoge.html"

r = requests.get( url )
soup = BeautifulSoup(r.text, 'lxml')
finded = soup.find_all("タグ") # 該当をシーケンスで取得
```

要素は文字列だけどstr型じゃないからキャストしてから検索する

<a id="application7"></a>

## 正規表現

reモジュールを使う

``` Python
import re

searched = re.find_all( "検索文字列", "被検索文字列" ) # 結果リスト
```

検索文字列に関して正規表現を使える

<a id="application8"></a>

## プログラム中からUnixコマンドを実行

``` python
import subprocess

catch = subprocess.call("clear") # clearコマンドを実行
catch = subprocess.call("ls") # lsを実行
```

標準でないコマンド(シェルスクリプトの自作コマンドなど)もすべて実行できる模様.

<a id="application9"></a>

## グラフ描写

<a id="application9"></a>

## 仮想環境構築

仮想環境の主な目的は,

- どっかのサーバーで運用するソフトウェアを作るときに必要なモジュールとバージョンを仮想環境からそのまま移行できて楽
- バージョン(Python本体でもモージュルでも)が標準のだと動かないこととかがあって, そういうときに仮想環境毎に違うバージョンを入れられる

みたいな感じ.

virtualenvを使って仮想環境を利用する.

``` sh
mkdir HogeProject # プロジェクトを作成
cd HogeProject # 仮想環境を作成
virtualenv hoge_env # 仮想環境に入る
# 作業をする
source hoge_env/bin/activate # 仮想環境から出る
deactivate
```
