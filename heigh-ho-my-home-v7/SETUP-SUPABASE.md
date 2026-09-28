# (最)(近) — Supabase setup

この v6 では、参加者が写真/文章を直接アップロードできる仕組みを用意しています。
サイト本体にファイルを保存するのではなく、Supabase Storage + Database を使います。

## 1. Supabase project
https://supabase.com/ で無料プロジェクトを作成。

## 2. Storage
Storage → New bucket → `recent`
- Public bucket: ON

## 3. SQL Editor
以下を実行：

```sql
create table public.recent_posts (
  id uuid primary key default gen_random_uuid(),
  type text not null check (type in ('image','text')),
  content text default '',
  image_url text default '',
  published boolean not null default true,
  created_at timestamptz not null default now()
);

alter table public.recent_posts enable row level security;

create policy "public can read published posts"
on public.recent_posts for select
to anon
using (published = true);

create policy "anyone can insert posts"
on public.recent_posts for insert
to anon
with check (published = true);

create policy "anyone can upload recent images"
on storage.objects for insert
to anon
with check (bucket_id = 'recent');
```

※ 公開サイトから誰でも投稿できる設定なので、公開後に荒らし対策・削除方法などを追加したくなったら、この部分を強化します。

## 4. API keys
Supabase の Project Settings → API から
- Project URL
- anon / publishable key

をコピーして `participate/config.js` に入れます。

```js
window.SUPABASE_URL = "ここ";
window.SUPABASE_ANON_KEY = "ここ";
```

この anon key は公開サイトに置く前提のキーです。service_role key は絶対に入れないでください。

## 5. 動作
- `/participate/index.html` → 集まった「最近」からランダムに1件表示
- `/participate/upload.html` → 写真 / 文章を投稿
- `/participate/archive.html` → 全投稿を一覧
- `/participate/about.html` → プロジェクト説明

写真はアップロード前にブラウザ側で最大1600px・JPEG品質82%程度に縮小するので、そのまま巨大な写真を送るよりかなり軽くなります。

## ⑥ Heigh-Ho
歌詞はサイトに掲載せず、YouTubeへのリンクにしています。
現在は Disney Kids の動画を設定：
https://www.youtube.com/watch?v=sc3XjzyQP7A

別の曲に変える場合は `heigh-ho/index.html` の
`href="..."` のURLだけ変更してください。
