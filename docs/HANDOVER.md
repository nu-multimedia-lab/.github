# 引き継ぎ書（GitHub organization 運用）

最終更新：2026-11-22（作成：GardenTree / 元部長）

この org を、誰か一人がいなくなっても回る状態に保つためのルールです。
毎年の代替わり（学祭後の 11〜12 月ごろ）のときに、新旧部長でこのファイルを一緒に読んで更新してください。

---

## 1. 権限（Owner）

### 現在の Owner

| GitHub ID | 立場 | 備考 |
|---|---|---|
| suekkonosuzuki | 現役 | |
| teeeeeeen | 現役 | |
| Garden-Tree | OB（元部長） | 予備。困ったときの最終手段 |

### ルール

- Owner は常に 2〜4 人にする。1 人だけだと、その人が卒業したら誰も org を管理できなくなる。
- 現役 Owner は部長＋副部長（代替わり前後は新旧部長）が基本。
- Owner は 2FA（二要素認証）必須。
- 卒業する Owner は **後任を Owner にしてから** 自分を Member に下げる（順番を逆にしない）。
- それ以外のメンバーは Member でよい。Owner はリポジトリやメンバーを削除できるので、増やしすぎない。

### 変更方法

People → 対象者にチェック → 「N member selected ▾」→ Change role → Owner / Member

---

## 2. 年間スケジュール

| 時期 | やること | 担当 |
|---|---|---|
| 4 月 | 新入生を org に招待 | 部長 |
| ゲームジャム開始時 | テンプレートからリポジトリを作る（命名ルールに沿う） | 各チームリーダー |
| ゲームジャム終了時 | 公開する作品は Releases と unityroom に出す（[RELEASE_GUIDE](RELEASE_GUIDE.md)）／[org トップページ](../profile/README.md) に追記 | 各チームリーダー |
| 10 月中旬（学祭前） | 展示する作品を Releases から落とせる状態にしておく（学祭は例年 10 月後半〜11 月初め） | 部長 |
| 11〜12 月（学祭後の代替わり） | Owner の交代／このファイルの更新／不要になったテスト用リポジトリを Archive | 新旧部長 |

### 卒業生の扱い

- 卒業生は org から外さず、Member のまま残す（作品の履歴に名前が残り、困ったときに相談もできるため）。
- 卒業する Owner は後任を Owner にしてから Member に下げる（1 章のルール）。

---

## 3. リポジトリのルール

### 命名

```
gamejam-<西暦>-<spring|summer|autumn|winter>-<チーム記号>
例）gamejam-2027-spring-A
```

- 過去のリポジトリ（`2024-03_gamejam_gt`、`2025_spring_B` など）は名前がバラバラだが、無理に直さなくてよい。新しく作るものからこのルールに従う。
- ゲームジャム以外の作品：作品名を英小文字とハイフンで書く（例：`dango-ninja`）

### 作るときに必ずやること

1. [unity-game-template](https://github.com/nu-multimedia-lab/unity-game-template) を開き、「Use this template」→「Create a new repository」で作る（Owner は nu-multimedia-lab、visibility は Private）
2. Description（リポジトリの説明文）を書く
3. README の（ ）の部分を書き換える

詳しい手順と、チームでの開発の進め方は [GitHub の使い方](GITHUB_GUIDE.md) を参照。

テンプレートには、Unity 用の `.gitignore` と `.gitattributes`（Git LFS）、README の雛形、自動リリースの workflow が入っている。テンプレートを使わずに作った場合は、これらを自分で入れる。

### 公開（public）・非公開（private）

- デフォルトは private。
- public にするのは、[RELEASE_GUIDE の公開前チェック](RELEASE_GUIDE.md#0-公開前チェック必須) を満たしたときだけ。
- 特に **Asset Store の有料アセットを含むリポジトリは public にしない**（規約違反になる可能性が高い）。

### この .github リポジトリの更新

- main ブランチには直接 push できない。作品の追加もドキュメントの修正も PR で出す。
- 承認は不要で、出した本人がマージしてよい。PR にすることで、誰がいつ何を変えたかの履歴が残る。
- PR の出し方は [RELEASE_GUIDE の 4 章](RELEASE_GUIDE.md#4-公開したら) を参照。

### Archive（読み取り専用化）

- 使わなくなったテスト用リポジトリや、開発が終わったリポジトリは削除せず Archive する。
- Settings → 一番下の Danger Zone → Archive this repository
- Archive はいつでも解除できる。削除は戻せないので、基本的に削除はしない。

---

## 4. 外部アカウント

サークルで共用しているアカウント。

| サービス | 用途 | アカウント | 備考 |
|---|---|---|---|
| Gmail | 各サービスの登録・ログイン用（GitHub org の請求先メールなど） | サークル共用 | アドレスとパスワードは Discord の役員_必読を参照 |
| unityroom | ゲームの Web 公開 | [nu-multimedia-lab](https://unityroom.com/users/nu-multimedia-lab) | 共用 Gmail の Google アカウントでログイン |
| X | 告知 | [@ecmultiple](https://x.com/ecmultiple) | 投稿は Discord の #sns で SNS 担当に依頼する |
| Instagram | 告知 | [@nagasakidaigakuml](https://www.instagram.com/nagasakidaigakuml/) | 同上 |
| Unity（自動ビルド用） | GitHub Actions でのビルド | 未定 | 自動ビルドを使うリポジトリごとに Owner が Secrets に登録。名義人が卒業するときは登録し直す |

- **パスワードはこのファイルに書かない**（このリポジトリは public）。ログイン情報は Discord の役員向けチャンネル（役員_必読 など）で管理する。
- GitHub 以外の引き継ぎ（サーバー管理・イベント・部活動継続願など）は、Discord の「引き継ぎ資料メモ」にまとまっている。
- 個人のクレジットカードで有料サービスを契約しない。卒業と同時に止まる原因になる。

---

## 5. 現在の状態メモ（2026-11 時点）

- メンバー 37 人、リポジトリ 19 個（うち public は `.github` と muse_port）
- `github_test` / `github-test-2025` / `github_branch` は Archive 済み
- ゲーム用テンプレート `unity-game-template` を作成済み
- muse_port（作品投稿サイト）：開発停止中。扱いは保留。
  - 構成：Next.js + FastAPI。Vercel と AWS Lambda にデプロイしていた（今も動いているかは未確認）
  - 再開しない場合は、先に Vercel と AWS を止めてから Archive する（課金や名義が残らないように）

---

## 6. 相談先

- まず Owner の誰かに相談
- 最終手段として OB の Garden-Tree に連絡
