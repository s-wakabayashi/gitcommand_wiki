# clone
**リポジトリをクローンする**
```
git clone git@github.com:noronaoki/git-command.git
```

# log
**履歴を表示する**
```js
git log

/*
━━ 表示 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
commit ee2b7d714426fd467f99a4c20b0ce272ed8215d2
Author: Kentaro Aoki <k-aoki@K-AOKI-WI7.voyagegroup.local>
Date:   Mon Apr 20 15:36:50 2015 +0900

    もう一度タイトル間違えた

commit 1dd1a1fd987d168463c72e186b3889cc95a5cff6
Author: Kentaro Aoki <k-aoki@K-AOKI-WI7.voyagegroup.local>
Date:   Mon Apr 20 15:35:47 2015 +0900

    Revert "Revert "title間違えた""
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*/
```
**履歴を1行で表示する**
```js
git log --oneline

/*
━━ 表示 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
555309f naosita
24e9411 Revert "もう一度タイトル間違えた"
ee2b7d7 もう一度タイトル間違えた
1dd1a1f Revert "Revert "title間違えた""
13dae75 Revert "title間違えた"
7a2aa8e title間違えた
5905772 Revert "改行幅を修正。"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*/
```




# reflog
**全ての履歴を表示する**
>いかなるブランチからもいかなるタグからも参照されていない更新内容であってもその時点に戻ることができます。  
>履歴を書き換えた後であっても reflog にはブランチの過去の状態が記録されており、必要な場合にはそこに戻ることができます。

```js
git reflog

/*
━━ 表示 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ef1f900 HEAD@{0}: head^^^^: updating HEAD
6ebb02d HEAD@{1}: commit: 修正漏れがあった。
99a7983 HEAD@{2}: commit: バグフィックスした。
f63f70b HEAD@{3}: commit: すばらしい機能を追加した。
68da592 HEAD@{4}: commit: 機能を拡張した。
ef1f900 HEAD@{5}: commit: 基本的な機能を実装した。
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*/
```
**特定の履歴に戻す**  
```js
// 「f63f70b HEAD@{3}: commit: すばらしい機能を追加した。」まで戻したい場合
git reset --hard HEAD@{3}
```

# merge
**リポジトリの変更を現在のブランチにマージ（統合）する**
```js
// 現在のブランチにdevを統合したい場合
git merge dev
```


# fetch
**リポジトリから変更点を取得する（マージはしない）**
```
git fetch
```


# pull
**リポジトリの内容をフェッチして、現在のブランチにマージする**  
fetchとmergeの合わせ技みたいなもの

```
git pull
```

# add
**変更をインデックスに追加する**
```js
// index.htmlを追加する場合
git add index.html
```
```js
// 全ての変更をインデックスに追加する場合
git add .
```

# commit
**インデックスに追加されている変更をコミットする**
```js
// インデックスにある状態を全てコミット
git commit -m '表示崩れを修正'
```
```js
// インデックスを無視して指定したファイルをコミット
git commit -m 'お知らせ枠の追加' index.html
```
```js
// 直前に行ったcommitメッセージを修正する
git commit --amend -m 'commit漏れを修正した'
```
```js
// 直前に行ったcommitをやり直す
// style.cssのコミット漏れを修正する例
git add style.css
git commit --amend -m 'commit漏れを修正した'
```

# push
**コミットしたものをリモートリポジトリに反映する**
```js
// ローカルリポジトリのdevブランチでリモートリポジトリのdevを更新する
git push origin dev:dev
```
```js
// ローカルリポジトリのdevブランチを削除  
git branch -d dev
```
```js
// リモートリポジトリのdevブランチを削除
git push :dev
```


# status
**作業ディレクトリの状態を表示する**
```js
// 作業ツリー、インデックス、HEADのステータスを確認
git status
```


# diff
**変更の差分を表示する**
```js
// 作業ツリーとインデックスの差分
git diff
```
```js
// インデックスとHEADの差分
git diff --cached
```
```js
// 作業ツリーとHEADの差分
git diff HEAD
```


# reset（uncommit(alias））
**特定のコミットまで戻る（pushする前のみ使える）**  
目的別のオプションが3つあるので注意して使い分ける

* --soft
    * HEADの位置のみ変更する
* --mixed（省略可）
    * HEADとインデックスの位置を変更する
* --hard
    * HEADとインデックスと作業ツリーの位置を変更する

* 【仕様上の注意】
    * resetはpushしたあとはやってはいけない 

### --soft
```js
// 1つ前のコミットまでHEADを戻す（インデックスにaddされたまま）
// 直前に行ったコミットをやり直したい時なんかに使える
git reset --soft HEAD^
```

### --mixed（省略可）
```js
// 1つ前のコミットまでHEADとインデックスを戻す（インデックスにaddも取り消される）
git reset HEAD^
```
```js
// 1つ前でファイルを全てaddしたが、index.htmlだけインデックスから取り除きたい
git reset HEAD^ index.html
```
### --hard
```js
// 1つ前のコミットまでHEADとインデックスと作業ツリーを戻す
// 作業ツリーも戻ってしまうので注意が必要
git reset --hard HEAD^
```


# revert
**特定のコミットを打ち消し、コミットする（push前/push後どちらにも使える）**
```js
// 最新のコミットを打ち消す
git revert HEAD
```
```js
// マージコミットの取り消し
git revert -m 1f60f24d
```

# rebase
**fast-fowardでmergeしたりコミットを改変する**
```js
// 過去のコミットをまとめるfix up
git rebase -i 2jfja0

/*
━━ 表示 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
pick 115127a common.jsを追加
pick 6c56e06 styleの変更
pick aed0e8a main.css追加

↓pickの部分をfに変更

pick 115127a common.jsを追加
f 6c56e06 styleの変更
f aed0e8a main.css追加

↓fにした部分が1つ前のコミットにまとめられる

pick 115127a common.jsを追加
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*/
```

```js
// 過去のコミットをまとめてコメントも編集するsquash
git rebase -i 2jfja0

/*
━━ 表示 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
pick 115127a common.jsを追加
pick 6c56e06 styleの変更
pick aed0e8a main.css追加

↓pickの部分をsに変更

pick 115127a common.jsを追加
s 6c56e06 styleの変更
s aed0e8a main.css追加

↓sにした部分が1つ前のコミットにまとめられるエディタが起動し、編集

pick 115127a common.jsを追加
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
*/
```

# branch
```js
// 現在のブランチを見る
git branch
```
```js
// ローカル・リモートの全てのブランチを見る
git branch -a
```
```js
// ローカルにdevブランチを新規作成
git branch dev
```
```js
// ローカルのdevブランチを削除
git branch -d dev
```
```js
// リモートのdevブランチを削除
git push origin :dev
```

# checkout
```js
// 作業ブランチをdevに切り替え
git checkout dev
```

# rm
```js
// ワーキングツリーとインデックスからindex.htmlを削除
git rm index.html  
```

# mv
```js
// index.htmlをtop.htmlにリネーム
git mv index.html top.html
```


# stash
```js
// ワーキングツリーの状態を退避(仮保存)する
// saveはオプションなので付けなくてもいい
git stash save '怖いからとっておく'
```
```js
// stashのリストを取得
git stash list
```
```js
// 指定したstashを現在のブランチに適用して削除
git stash pop stash@{1}
```
```js
// 指定したstashを削除
git stash drop stash@{2}
```
