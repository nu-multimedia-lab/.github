# 作品の公開手順（GitHub Releases / unityroom）

完成したゲームを誰でも遊べる状態にするための手順です。
就活のポートフォリオにもそのまま使えます。

公開先は 2 つ。どちらか片方だけでも OK です。

| 公開先 | 形式 | 向いている人 |
|---|---|---|
| GitHub Releases | Windows 版を zip でダウンロード | 重い 3D ゲーム、WebGL で動かないもの |
| unityroom | ブラウザでそのまま遊べる（WebGL） | 軽めのゲーム。見てもらいやすい |

---

## 0. 公開前チェック（必須）

公開する前に、**チーム全員で** 以下を確認してください。1 つでも ✗ があれば公開しない。

- [ ] チーム全員が公開に同意している（Discord で一言確認でよい）
- [ ] クレジットに載せる名前（本名 / ハンドルネーム）を各自が決めた
- [ ] 使用素材（画像・音楽・効果音・フォント・3D モデル）の利用規約で、再配布・公開が許可されている
- [ ] 素材のクレジット表記が README（とゲーム内）にある
- [ ] API キー・パスワードなどがリポジトリやビルドに含まれていない

### リポジトリ自体を public にする場合の追加チェック

ビルドだけ公開するなら不要。ソースコードまで public にする場合だけ確認。

- [ ] **Asset Store の有料アセットが、過去のコミットも含めて一度も入っていない**
  - public にすると過去のコミットも全部見える
  - 一度でも入れたことがあれば、リポジトリは private のままにして、ビルドだけ公開する

---

## 1. バージョンを決める

```
v1.0.0   … ゲームジャム提出版
v1.0.1   … バグ修正
v1.1.0   … 機能追加
```

---

## 2. GitHub Releases に Windows 版を置く

### 2-0. 自動ビルドを使う場合

[unity-game-template](https://github.com/nu-multimedia-lab/unity-game-template) から作ったリポジトリでは、タグを push するだけで Windows 版と WebGL 版がビルドされ、Releases に zip で添付されます。2-1〜2-3 の手作業は要りません。

```bash
git tag v1.0.0
git push origin v1.0.0
```

進み具合はリポジトリの「Actions」タブで見られます。終わると Releases に `リポジトリ名_v1.0.0_StandaloneWindows64.zip` と `…_WebGL.zip` が並びます。WebGL の zip は展開して unityroom にアップロードします（3 章）。

#### 最初に一度だけ：Unity ライセンスの登録（Owner の作業）

自動ビルドには Unity のライセンスが要ります。org の Secrets に一度登録すれば、全リポジトリで使えます。

1. 名義にする人が Unity Hub にログインし、Preferences → Licenses →「Add」→「Get a free personal license」でライセンスを追加する
2. ライセンスファイル `Unity_lic.ulf` を探す（隠しフォルダにある）
   - Windows：`C:\ProgramData\Unity\Unity_lic.ulf`
   - Mac：`/Library/Application Support/Unity/Unity_lic.ulf`
3. org の Settings → Secrets and variables → Actions →「New organization secret」で次の 3 つを登録する（Repository access は All repositories か Private repositories）
   - `UNITY_LICENSE`：`.ulf` ファイルの中身をそのまま貼る
   - `UNITY_EMAIL`：その Unity アカウントのメールアドレス
   - `UNITY_PASSWORD`：その Unity アカウントのパスワード
4. 登録したら Unity Hub からサインアウトする

名義人を [引き継ぎ書](HANDOVER.md#4-外部アカウント) に書いておき、卒業するときは後任の名義で登録し直します。

private リポジトリの Actions には、org 全体で月ごとの無料時間の上限があります。Unity のビルドは 1 回で数十分かかることがあるので、タグを打つのはリリースするときだけにします。

### 2-1. ビルド（手動の場合）

1. Unity で「File → Build Profiles」（古い Unity では Build Settings）を開く
2. Platform を「Windows」にする
3. 出力先を `Builds/Windows/` などにして Build

### 2-2. zip にする

出力フォルダの中身をフォルダごと zip にします。

```
MyGame_v1.0.0_Windows.zip
└── MyGame/
    ├── MyGame.exe
    ├── MyGame_Data/
    ├── UnityPlayer.dll
    └── ...
```

- `*_BurstDebugInformation_DoNotShip` というフォルダがあれば zip に入れない（配布不要）
- exe だけ渡しても動かないので注意

### 2-3. Release を作る

ブラウザで作る場合は、次の手順で進めます。

1. リポジトリのトップ → 右側の「Releases」→「Draft a new release」
2. 「Choose a tag」で `v1.0.0` を入力 →「Create new tag」
3. タイトル：`v1.0.0（2026 夏ゲームジャム提出版）` など
4. 説明に、遊び方・操作方法・動作環境を書く
5. zip を「Attach binaries」にドラッグ
6. 「Publish release」を押す

[gh](https://cli.github.com/) が入っていれば、次のコマンドでも作れます。

```bash
gh release create v1.0.0 MyGame_v1.0.0_Windows.zip \
  --title "v1.0.0（2026 夏ゲームジャム提出版）" \
  --notes "操作方法は README を参照"
```

> private リポジトリの Release は org メンバーしか見られません。
> 外部に配布したい場合は、リポジトリを public にする（0 章のチェック必須）か、unityroom を使ってください。

---

## 3. unityroom に WebGL 版を置く

### 3-1. ビルド設定

「File → Build Profiles」で Platform を「Web（WebGL）」に切り替え、Player Settings → Publishing Settings を次の表のとおりにします（unityroom 公式ヘルプの指定）。

| 項目 | 設定 |
|---|---|
| Development Build | オフ |
| Compression Format | Gzip |
| Decompression Fallback | オフ |

最新の手順は unityroom 公式ヘルプ「unityroomにアップロードするためのビルド方法」を確認してください： https://help.unityroom.com/

### 3-2. よくあるハマりどころ

- 日本語が表示されない（□になる）
  → WebGL の標準フォントには日本語が入っていない。日本語フォント（例：Noto Sans JP）を入れて、TextMeshPro の Font Asset を作り直す。unityroom 公式ヘルプにも記事あり。
- 途中で止まる
  → WebGL では例外が出るとゲームが止まる。エディタで Console に赤いエラーが出ていないか確認。
- 重い・起動しない
  → テクスチャの Max Size を下げる、音声の圧縮品質を下げる、`Resources` フォルダに不要なものを置かない。
- エディタでは動くのに WebGL で動かない
  → WebGL では `Awake` / `Start` が呼ばれる順番がエディタと変わることがある。呼ばれる順番を前提にした初期化をしていないか確認。

### 3-3. 投稿

1. unityroom にログイン → 「ゲームを登録」
2. ゲーム情報（タイトル・説明・操作方法・サムネイル）を入力
3. WebGL アップロード画面で、ビルドで出力されたファイルを、拡張子を間違えずにアップロード
4. 自分でプレイして動作確認 → 一般公開

> アカウントをサークル共用にするか各自にするかは [引き継ぎ書](HANDOVER.md#4-外部アカウント) を確認。

---

## 4. 公開したら

1. ゲームリポジトリの README に unityroom と Releases のリンクを追記
2. リポジトリの About（右上の歯車アイコン）の Website 欄に unityroom の URL を入れる
3. org トップページ（[`profile/README.md`](../profile/README.md)）の作品一覧に 1 行追加する PR を出す（手順は下記）
4. Discord で報告する

### org トップページに作品を追加する PR の出し方

main には直接書き込めないので、PR で出します。ブラウザだけでできます。

1. [`profile/README.md`](../profile/README.md) を開き、右上の鉛筆アイコン（Edit this file）を押す
2. 「遊べる作品」の表の、コメント行のすぐ下に 1 行追加する（新しい作品を上に）
3. 「Commit changes...」を押し、「Create a new branch for this commit and start a pull request」を選んで「Propose changes」を押す
4. PR の画面で「Create pull request」を押す
5. 「Merge pull request」を押してマージする（承認は不要。自分でマージしてよい）
