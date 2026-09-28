# heigh-ho-my-home 編集ガイド

## 0. 基本の流れ

1. ZIPを解凍する。
2. `heigh-ho-my-home-v7` フォルダの中で画像やHTMLを編集する。
3. 編集後、フォルダ全体をそのままサイト側へアップロードする。
4. すでに同名ファイルがある場合は上書きする。

※ ファイル名とフォルダ名は、基本的に今ある名前を変えない。

---

## 1. 画像を追加・差し替える

### Log
画像を入れる場所：
`blog/images/`

例：
`0810-01.jpg`
`0810-02.jpg`

HTML側では、該当日のページに以下のように追加する。

`<img src="images/0810-01.jpg" alt="">`

### Collect / things I found
現在は各ページから `../blog/images/...` を参照している。
別の画像を使いたい場合は、各ページの `<img src="...">` を差し替える。

対象：
- `collect/paper.html`
- `collect/accidents.html`
- `collect/details.html`

画像は縦長のものをそのまま入れてOK。ページ側で4列に整列する。

---

## 2. Logを新しく追加する

例：2026/08/10のLogを追加したい場合

### A. 過去のHTMLをコピー
`blog/0731.html` をコピーして、
`blog/0810.html` にする。

### B. 中身を変更
以下を変更する。
- `<title>`
- 日付
- 本文
- 写真のファイル名

### C. 写真を入れる
`blog/images/0810-01.jpg` などを入れる。

### D. Log一覧に追加
`blog/index.html` を開き、日付リンクを1行追加する。

例：
`<a href="0810.html">2026/08/10</a>`

---

## 3. ⑤ things I found のタイトル画像

共有ファイル：
`collect/images/collect-title.svg`

この1ファイルを、
- ホーム⑤
- `collect/index.html` の下層トップ

の両方で使っている。

### Illustratorで自分のタイトル画像を作ったら
1. Illustratorでタイトルを作る。
2. SVGで書き出す。
3. ファイル名を **`collect-title.svg`** にする。
4. `collect/images/collect-title.svg` を上書きする。
5. サイト側にも同じファイルをアップロードして上書きする。

つまり、HTMLを触らなくてもタイトル画像だけ差し替えられる。

---

## 4. Experimentのタイトル画像

共有ファイル：
`experiment/images/experiment-title.svg`

このファイルはExperimentのトップと詳細ページで共通使用。

Illustratorで差し替える場合は、同じファイル名 `experiment-title.svg` で書き出して上書きする。

---

## 5. Experimentの内容を追加する

トップ一覧：
`experiment/index.html`

詳細ページ：
- `experiment/detail-01.html`
- `experiment/detail-02.html`
- `experiment/detail-03.html`

今の詳細ページには画像用の空箱がある。
実際の画像を入れるときは、HTML内の `.detail-image` 部分を画像タグに変更する。

例：
`<img class="detail-image" src="images/experiment-01.jpg" alt="">`

画像ファイルを `experiment/images/` に入れる。

---

## 6. ⑦ ????? の6つの実験

トップ：
`room-07/index.html`

詳細：
- `room-07/experiment-01.html`
- `room-07/experiment-02.html`
- `room-07/experiment-03.html`
- `room-07/experiment-04.html`
- `room-07/experiment-05.html`
- `room-07/experiment-06.html`

今は各ページがプレースホルダー状態なので、ここに好きな実験内容を入れていく。

---

## 7. ⑧ (最)(近) の設定

### 最初に一度だけやること
`SETUP-SUPABASE.md` の手順に沿ってSupabaseを設定する。

設定後、
`participate/config.js`

に以下の2つを入れる。
- Supabase Project URL
- anon / publishable key

**service_role keyは絶対に入れない。**

### 投稿
`participate/upload.html` から写真または文章を投稿する。

投稿されたものはSupabaseに保存され、
- `participate/index.html` → ランダムに1件表示
- `participate/archive.html` → 全件表示

となる。

---

## 8. ⑨ Profile

ページ：
`room-09/index.html`

文章を変更したい場合は、このHTML内の `.profile-text` の文章を変更する。

ホームの⑨は、この文章を大きくした状態をクリッピングして表示している。
ホーム上では縦・横にスクロールできる。

---

## 9. ホームの仕掛けを変更する

ホーム本体：
`index.html`

共通スタイル・動き：
`style.css`

現在の動き：
- ① 動かない
- ② 拡大＋縦横スクロール
- ③ 拡大＋縦横スクロール
- ④ Logが回転
- ⑤ タイトル画像
- ⑥ ♪がリズムに合わせて上下
- ⑦ 5つの?がランダムな順番で点滅
- ⑧ 動かない
- ⑨ プロフィールを拡大＋縦横スクロール

ホームの文字・リンク先を変えるときは `index.html`。
見た目やアニメーションを変えるときは基本的に `style.css`。

---

## 10. 迷ったら

「画像を変えたい」→ まず画像ファイルを探す

「文章を変えたい」→ 該当する `.html` を探す

「タイトル画像を変えたい」→ SVGファイルを同じ名前で上書き

「動きを変えたい」→ `style.css` または `index.html` の `<script>`

「新しい部屋を作りたい」→ まずChatGPTに「⑩をこうしたい」と伝えればOK。
