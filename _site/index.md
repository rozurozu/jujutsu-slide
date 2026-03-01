---
marp: true
theme: gaia
class:
  - invert
style: |
  .red { color: #ff4b4b; }
  .blue { color: #1e90ff; }
---

<style scoped>
  /* 右下に情報をまとめるコンテナ */
  .profile {
    position: absolute;
    bottom: 40px;
    right: 50px;
    text-align: right;
    font-size: 22px;
  }
  /* GitHubロゴ風の調整（画像URLは公式のものなどを使用） */
  .github-id {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 10px;
    font-weight: bold;
    margin-top: 5px;
  }
  .github-id img {
    width: 32px;
    height: 32px;
  }
</style>

# **jujutsu(jj) の良さみ**

<div class="profile">
  Created:2026-02-28<br>
  Updated:2026-02-28<br>
  v1.0.0
  <div class="github-id">
    <img src="images/icons/github.png">
    @rozurozu
  </div>
</div>

---

<style scoped>
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .square-box {
    display: flex;
    gap: 40px; /* 画像の間隔 */
    margin-bottom: 20px;
  }
  .square-box img {
    width: 300px;
    height: 300px;
    object-fit: cover;
  }
</style>

## **jujutsu(jj) とは**<br>

git互換のバージョン管理ツール<br>
<br>

<div class="square-box">
  <img src="images/icons/jj.png">
  <img src="images/icons/git.png">
</div>

---

## **コマンドは `jj`**

`jj`
`jj new`
`jj desc`
`jj b s`
`jj squash`
`jj rebase`
<br><br>

### `jj`って打ちやすいし、**イケてる**

---

## **自動保存**

### 変更は常に、最新のコミットに反映される

- **git**：未保存の作業を、明示的に**コミット**という箱へ入れる
- **jj**：最新**コミット**という箱の中で、直接作業をする。

<br><br>

### Gitにおける『保存（<span class="red">Commit</span>）』という儀式を、Jujutsuは<span class="red">自動化</span>した

---

## **stash不要**

![bg right:40% fit](images/no-stash.png)

#### `jj new`コマンド

新たなコミットを作成し、HEADを移す。

feature/add-snsブランチをレビューしてください！って言われた時の操作

`jj new feature/add-sns@origin`

---

## **ブランチが切りやすい！**

<style scoped>

  .split-content {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-top: 20px;
  }

  .text-box {
    width: 38%;
  }

  .image-box {
    width: 60%; /* 画像側の幅 */
    margin-top: 40px; /* 画像を少し下にずらす調整 */
  }

  .image-box img {
    width: 100%;
    border-radius: 8px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  }

  .red {
    color: #ff4b4b;
    font-weight: bold;
  }
</style>

<div class="split-content">
<div class="text-box">

`jj log`コマンドで
ツリーが表示される。

チェンジID：<span class="red">x</span>ukpltwo

このチェンジから
ブランチ分岐したい時、
`jj new x`コマンドで...

</div>
<div class="image-box">

![fit](images/jj-new-01.png)

</div>
</div>

---

<style scoped>

  .split-content {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-top: 20px;
  }

  .text-box {
    width: 38%;
  }

  .image-box {
    width: 60%; /* 画像側の幅 */
    margin-top: 40px; /* 画像を少し下にずらす調整 */
  }

  .image-box img {
    width: 100%;
    border-radius: 8px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  }

  .red {
    color: #ff4b4b;
    font-weight: bold;
  }
</style>

<div class="split-content">
<div class="text-box">

<span class="red">x</span>ukpltwo
から
<span class="blue">v</span>orlmqus
が分岐した！

**ブランチ名も不要！**
**チェンジの指定が簡単！**

</div>
<div class="image-box">

![fit](images/jj-new-02.png)

</div>
</div>

---

## **`undo` 最強！！**

一つ前の操作をキャンセル出来る！
例えばrebaseをミスした時

---

### gitの場合

rebaseミスった！
→ `git reflog`でどこまで戻ればいいか確認
→ `git reset --hard HEAD{n}`
<br><br><br><br>
💡 補足：
`HEAD`じゃなくて`ORIG_HEAD`で操作前を指定できるらしいw

---

### jujutsuの場合

rebaseミスった！

## → `jj undo`

## <span class="red">**これだけ！**</span>

<br>

💡 補足：
操作を複数戻したい時は`jj undo`しまくればいい！
戻りすぎた時には`jj redo`で、やり直せる！

---

### **コンフリクトしても作業続行**

![fit](images/conflict01.png)

**こんにちわ** を **hello** にリベース
![fit](images/conflict02.png)

---

![fit](images/conflict03.png)

コンフリクトマーカーを持ったままコミットされている
![fit](images/conflict04.png)

---

`jj new`で作業を続けれる！
コンフリクトは後で解消すれば良い！
![fit](images/conflict05.png)

---

## **後で綺麗にすればいい**

なんとなく**git**では、毎回のコミットに神経質になる。
`git rebase -i`は便利だけど、コンフリクトの不安は付きまとう。

コーディングエージェントでの開発で、毎回全行レビューはしない。
一旦こんなもんか、でセーブしたい。
こっちの方法だとどうだろうでやり方を分岐させたり。

プッシュする前に綺麗にすればいいじゃない

**チェンジは気軽なセーブポイント**

---

## **まとめ**

- 自動保存！単純明快！
  作業ツリー、インデックス、コミットなんていらない！
- だから、`stash`も不要！
- 最強コマンド！ `jj undo`
- コンフリクトしててもコミット可能！

普段から、過去のコミットの修正や履歴を操作する人にはおすすめ！
コーディングエージェント使う人にもおすすめ！
まだ情報もツールも少ないからgitでいいかもw **<span class="red">学習コスト</span>＞<span class="blue">メリット</span>**

---

## **おまけ よく使うコマンド**

- `description`または`desc`
  コミットメッセージを付与する。
- `commit -m`
  `desc` + `new`と同じ。めちゃ使う。
- `bookmark set`または`b s`
  bookmarkを移動させるときに使う。めちゃ使う。
- `squash`
  　めちゃ使うからエイリアス`sq`にしてる
  他にも、`rebase`, `workspace`, `abandon`, `jj git fetch`, `jj git push`

---

## **学習コストは少し高いかも🤯**

- **チェンジ**の概念が少しだけ難しい
- 日本語の情報が少ない
- ツールも少ない
- 公式のcliリファレンスが正確じゃない？らしい
  > This CLI reference is experimental. It is automatically generated, but does not match the jj help output exactly.

https://docs.jj-vcs.dev/latest/cli-reference/#jj-workspace
