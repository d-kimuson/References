# Githubメモ

## 初期設定

```sh
$ ssh-keygen -t rsa
```

で, 生成された公開鍵: ~/.ssh/id_rsa.pub の中身をGithubに渡す

## リモートリポジトリとローカルの紐付け

### 1. git clone で コピってくる

``` sh
$ git clone <リポジトリURL> <ディレクトリ名>
```

### 2. ディレクトリを作成して, remote add origin \<URL\>

``` sh
$ git init
$ git add <編集したファイル/ディレクトリパス>
$ git commit -m "コメント"
$ git remote add origin <リポジトリURL>
$ git push origin master
```

## Gitコマンド

| コマンド | 内容 |
|:---:|:---:|
| add | ファイルの変更点をステージング |
| commit | ステージングされた内容をローカルに反映 |
| push | ローカルをリモートに反映 |
| branch | ブランチのリストを表示 |
| branch <ブランチ名> | ブランチ作成 |
| checkout <ブランチ名> | ブランチへ移動 |
| git merge | ブランチを結合 |
| git fetch | リモート -> origin/masterへ反映 |

### ローカル→Githubへ

``` sh
$ git add <編集したファイル/ディレクトリパス>
$ git commit -m "コメント"
$ git push origin <ブランチ>
```

### pull request

1. (Github上で)Compare pull request
2. プルリクする/されるブランチを選択(base → add-new-file)
3. Merge pull requestで完了


### ローカルリポジトリの最新化

``` sh
$ git fetch
$ git merge origin/master
```
