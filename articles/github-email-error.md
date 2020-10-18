---
title: 'githubのpush時のprivate email関係のエラーを解消する方法'
emoji: '🤖'
type: 'tech'
topics: ['github']
published: true
---

# github の push 時の private email 関係のエラーを解消する方法

## First

今まで普通に push できていたはずなのに，ある日突然 github の push 時に以下のエラーが起きて push できなくなった．  
**remote: error: GH007: Your push would publish a private email address.**

## Why

github の設定で自分の email を private にするみたいな設定をしたようで，それで config に自分の email アドレスを設定している状態で push しようとしているのでエラーが出ているようだ．  
ちなみに github で private に設定している場所は Settings の Emails の以下のチェックボックスにチェックしているからだと思われる．

**Keep my email addresses private**

## Resolution

### commit から push しようとしてエラーに気づいた場合

`git reset --soft HEAD^`などをして一度 commit を取り消しておきます．これで`git add`をした状態にまで戻りました.

### email の変更

github の Setting の Emails，**Keep my email addresses private**の文章中に\"\<数字 8 桁くらい\>+\<ユーザ名\>@users.noreply.github.com\"みたいなアドレスがあると思うので，これをコピーする．  
そして以下のコマンドで email の config を変更する．

```shell
git config --global user.email "コピーしたアドレス"
```

### 再び commit そして push

あとは add して commit して push です．

## Finally

たった 1 つの設定変更ですが，いきなり起きると訳が分からず苦労したので，もし同じような方がいたら試してください．  
ちなみに時間をおいて私は 2 回経験しました．  
2 回目はそこまで時間をかけずに解消しましたが，それでも以前どうやって解決したか忘れてあたふたしました．(だから記事をかいておこうとした訳です笑)

---

## References

- https://blog.proglus.jp/1310/
- https://qiita.com/Canon11/items/e6f64597d82dbf88f75f
- https://ontheneworbit.blogspot.com/2018/03/githubpush-your-push-would-publish.html

## Change log

- 2020/10/20: 見出し「おわりに」を「Finally」に変更\(なぜ最後だけ日本語にしたか自分でも分からない笑\)
- 2020/10/20: References 追加\(項目を忘れていました\)
