# 引き継ぎ書（GitHub organization 運用）

最終更新：2026-11-22（作成：GardenTree / 元部長）

この org を、誰か一人がいなくなっても回る状態に保つためのルールです。
毎年の代替わりのときに、新旧部長でこのファイルを一緒に読んで更新してください。

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
- 現役 Owner は部長＋次期部長（または副部長）が基本。
- Owner は 2FA（二要素認証）必須。
- 卒業する Owner は **後任を Owner にしてから** 自分を Member に下げる（順番を逆にしない）。
- それ以外のメンバーは Member でよい。Owner はリポジトリやメンバーを削除できるので、増やしすぎない。

### 変更方法

People → 対象者にチェック → 「N member selected ▾」→ Change role → Owner / Member

Owner を交代したら、この `.github` リポジトリの `CODEOWNERS` に書いた ID も PR で書き換える（承認者がいなくなるのを防ぐため）。

---

## 2. 年間スケジュール

| 時期 | やること | 担当 |
|---|---|---|
| 4 月（代替わり） | Owner の交代／このファイルの更新／新入生を org に招待 | 新旧部長 |
| 4 月 | 卒業生の扱いを決める（残す or 外す）※下記 | 部長 |
| ゲームジャム開始時 | 命名ルールに沿ってリポジトリ作成、README 雛形を入れる | 各チームリーダー |
| ゲームジャム終了時 | 公開する作品は Releases と unityroom に出す（[RELEASE_GUIDE](RELEASE_GUIDE.md)）／[org トップページ](../profile/README.md) に追記 | 各チームリーダー |
| 学祭前 | 展示する作品を Releases から落とせる状態にしておく | 部長 |
| 年度末 | 不要になったテスト用リポジトリを Archive | Owner |

### 卒業生の扱い

- 基本は Member のまま残してよい（作品の履歴に名前が残るため）。
- 長期間使っていない・連絡が取れないアカウントは、年度末に外してよい。
- 外しても、そのアカウントのコミット履歴は消えない。

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

1. Description（リポジトリの説明文）を書く
2. `README.md` を [テンプレート](../templates/GAME_README.md) から作る
3. Unity 用の `.gitignore` と `.gitattributes`（Git LFS）を入れる

### 公開（public）・非公開（private）

- デフォルトは private。
- public にするのは、[RELEASE_GUIDE の公開前チェック](RELEASE_GUIDE.md#0-公開前チェック必須) を満たしたときだけ。
- 特に **Asset Store の有料アセットを含むリポジトリは public にしない**（規約違反になる可能性が高い）。

### この .github リポジトリの更新

- main ブランチには直接 push できない。作品の追加もドキュメントの修正も PR で出す。
- マージには、`CODEOWNERS` に書いた Owner のうち 1 人の承認が要る。
- PR の出し方は [RELEASE_GUIDE の 4 章](RELEASE_GUIDE.md#4-公開したら) を参照。

### Archive（読み取り専用化）

- 使わなくなったテスト用リポジトリや、開発が終わったリポジトリは削除せず Archive する。
- Settings → 一番下の Danger Zone → Archive this repository
- Archive はいつでも解除できる。削除は戻せないので、基本的に削除はしない。

---

## 4. 外部アカウント

| サービス | 用途 | 名義 | 備考 |
|---|---|---|---|
| unityroom | ゲームの Web 公開 | （サークル共用アカウント or 各自） | 決まったら記入 |
| （共用 Gmail） | 各サービスの登録用 | サークル | 作成したら記入 |

- **パスワードはこのファイルに書かない。** 共有パスワードマネージャー（Bitwarden の組織機能など）で管理し、部長・副部長に引き継ぐ。
- 個人のクレジットカードで有料サービスを契約しない。卒業と同時に止まる原因になる。

---

## 5. 現在の状態メモ（2026-11 時点）

- メンバー 37 人、リポジトリ 17 個（うち public は muse_port のみ）
- `github_test` / `github-test-2025` / `github_branch` は Archive 済み
- muse_port（作品投稿サイト）：開発停止中。扱いは保留。
  - 構成：Next.js + FastAPI。Vercel と AWS Lambda で動いている
  - 再開しない場合は、先に Vercel と AWS を止めてから Archive する（課金や名義が残らないように）

---

## 6. 相談先

- まず Owner の誰かに相談
- 最終手段として OB の Garden-Tree に連絡
