# GitHub の使い方（Unity でのチーム開発）

サークルで Unity のゲームを複数人で作るための、GitHub の使い方をまとめています。
初めての人は 1 章から順番に進めてください。

画面のスクリーンショット付きの手順は、元部長の記事
[【Unity】SourceTree/VSCodeを用いた複数人開発の方法【GitHub】（ガデログ）](https://gadelog.com/%E3%80%90unity%E3%80%91%E8%A4%87%E6%95%B0%E4%BA%BA%E9%96%8B%E7%99%BA%E3%81%AE%E6%96%B9%E6%B3%95%E3%80%90github%E3%80%91/)も参考になります。
記事の手順と違うのは、サークルではテンプレートからリポジトリを作る点です（3 章）。

---

## 1. 準備（最初に一度だけ）

### 1-1. GitHub アカウントを作り、org に入る

1. [GitHub](https://github.com/) でアカウントを作る
2. Owner（部長など）に GitHub の ID を伝えて、nu-multimedia-lab に招待してもらう
3. 届いた招待メールか、GitHub の通知から招待を承認する

### 1-2. ツールを入れる

| ツール | 用途 | 入れるときの注意 |
|---|---|---|
| [Git](https://git-scm.com/) | 変更履歴を管理する | インストールの途中で、デフォルトのエディタを VSCode に、デフォルトのブランチ名を `main` にする |
| Git LFS | 画像や音声などの大きいファイルを扱う | Windows の Git には同梱されている。Mac は Homebrew で `brew install git-lfs` を実行して入れる。どちらも、入れたあとに一度だけターミナルで `git lfs install` を実行する |
| [Visual Studio Code](https://code.visualstudio.com/) | コードを書く・Git を操作する | 拡張機能「Unity」と「Japanese Language Pack」を入れる |
| Unity Hub と Unity | ゲームを作る | Unity のバージョンはチーム全員でそろえる（3 章） |

### 1-3. Unity と VSCode をつなぐ

Unity の Edit → Preferences → External Tools で、「External Script Editor」を「Visual Studio Code」にします。これで、Unity からスクリプトを開くと VSCode が立ち上がります。

---

## 2. Git の基本

| 言葉 | 意味 |
|---|---|
| リポジトリ | プロジェクトのファイルと変更履歴の入れ物。GitHub 上のものを「リモート」、自分の PC にあるものを「ローカル」と呼ぶ |
| クローン | リモートのリポジトリを自分の PC にコピーする |
| コミット | 変更をひとまとまりとして履歴に記録する（ローカルだけ） |
| プッシュ | ローカルのコミットを GitHub に送る |
| プル | GitHub にあるほかの人の変更を取り込む |
| ブランチ | 作業の枝分かれ。自分のブランチで作業して、あとで `main` にまとめる |
| プルリクエスト（PR） | 自分のブランチを `main` にまとめてよいか、チームに確認してもらう仕組み |

---

## 3. リポジトリを作る（チームリーダーの作業）

### 3-1. テンプレートから作る

1. [unity-game-template](https://github.com/nu-multimedia-lab/unity-game-template) を開き、「Use this template」→「Create a new repository」を押す
2. Owner を `nu-multimedia-lab` にし、名前を命名ルールに沿って付ける（例：`gamejam-2027-spring-A`。[引き継ぎ書](HANDOVER.md#命名) を参照）
3. visibility は Private にして作る

### 3-2. メンバーに書き込み権限を付ける

org に入っているだけでは、メンバーがプッシュできないことがあります。リポジトリの Settings → Collaborators and teams →「Add people」で、チームメンバーを Write 権限で追加してください。

### 3-3. Unity プロジェクトを入れる

テンプレートの `.gitignore` は、Unity プロジェクトがリポジトリの直下にある前提で書かれています。次の順番で入れてください。

1. VSCode の「ソース管理」→「リポジトリのクローン」で、作ったリポジトリを PC にクローンする
2. Unity Hub で新しいプロジェクトを作る（作る場所はどこでもよい）
3. できたプロジェクトフォルダの中の `Assets`、`Packages`、`ProjectSettings` の 3 つを、クローンしたフォルダの直下にコピーする
4. Unity Hub の「Add」→「Add project from disk」で、クローンしたフォルダを開く
5. Unity の Edit → Project Settings → Editor で、次の 2 つを確認する
   - Version Control の Mode：Visible Meta Files
   - Asset Serialization の Mode：Force Text
6. VSCode で変更をすべてコミットし、プッシュする

使った Unity のバージョン（`ProjectSettings/ProjectVersion.txt` に書かれている）を README に書き、メンバーに伝えます。

---

## 4. 開発に参加する（メンバーの作業）

1. VSCode の「ソース管理」→「リポジトリのクローン」で、リポジトリの URL（HTTPS）を入れてクローンする
2. Unity Hub で、README に書かれたのと同じバージョンの Unity を入れる
3. Unity Hub の「Add」→「Add project from disk」で、クローンしたフォルダを開く

初回は `Library` フォルダが作られるので、開くまで時間がかかります。

---

## 5. 毎日の作業の流れ

```
プル → 自分のブランチで作業 → コミット → プッシュ → PR → main にマージ
```

1. 作業を始める前に、VSCode 左下の同期ボタンを押して `main` をプルする
2. 左下のブランチ名（`main`）を押し、「新しいブランチを作成」で自分のブランチを作る。名前は `自分の名前` か `作る機能の名前`（例：`tanaka`、`player-move`）
3. 作業したら、ソース管理タブでメッセージを書いて、こまめに「コミット」する。メッセージには何をしたかを書く（例：「プレイヤーのジャンプを追加」）
4. 「変更の同期」または「ブランチの発行」を押してプッシュする
5. GitHub のリポジトリを開くと「Compare & pull request」が出るので押し、何を変えたかを書いて PR を作る
6. チームで決めたやり方（リーダーが確認する、本人がマージする など）で `main` にマージする
7. ほかの人は `main` をプルして、自分のブランチに取り込む

---

## 6. Unity で気をつけること

Unity のシーン（`.unity`）やプレハブ（`.prefab`）は、複数人が同時に編集すると、まとめるのがとても難しくなります。

- **同じシーンを同時に編集しない。** 触る前に Discord で「〇〇シーン触ります」と一声かける
- UI、ステージ、プレイヤーなどはプレハブに分け、それぞれの担当が自分のプレハブを編集する
- `.meta` ファイルも必ず一緒にコミットする。抜けると、スクリプトが外れたりマテリアルがピンクになったりする
- Unity のバージョンを勝手に上げない。上げるときはチームで決めて、全員で同時に上げる
- パッケージを追加・更新したら、チームに伝える（`Packages/manifest.json` が変わるため）
- ビルドしたファイル（`Builds/`）はコミットしない。配布は Releases を使う（[公開手順](RELEASE_GUIDE.md)）

---

## 7. コンフリクト（競合）が起きたら

同じファイルの同じ場所をほかの人も変えていると、プルやマージのときにコンフリクトが起きます。

- スクリプト（`.cs`）：VSCode でファイルを開くと、両方の変更が並んで表示されます。「現在の変更を取り込む」「入力側の変更を取り込む」「両方の変更を取り込む」から選ぶか、手で直して保存し、コミットします
- シーン・プレハブ：中身を手で直すのはおすすめしません。VSCode で「現在の変更を取り込む」か「入力側の変更を取り込む」をファイル全体に適用してどちらか一方のファイルを残し、残さなかった側の変更は Unity 上でやり直します

わからなくなったら、作業を止めて Discord の #プログラマー で相談してください。無理に進めると、ほかの人の作業を消してしまうことがあります。

---

## 8. よくあるトラブル

| 症状 | 原因と対処 |
|---|---|
| プッシュが拒否される（rejected） | GitHub に自分の持っていないコミットがある。先にプルしてから、もう一度プッシュする |
| 画像や音声が壊れている・開けない | Git LFS が入っていない。`git lfs install` を実行して、`git lfs pull` で取り直す |
| スクリプトが「Missing」になる・マテリアルがピンク | `.meta` ファイルがコミットされていない。作った人にコミットしてもらう |
| 100MB を超えるファイルがプッシュできない | GitHub は 1 ファイル 100MB までしか受け付けない。動画や素材の原本はリポジトリに入れず、Google ドライブなどで共有する |
| Unity で開くとエラーが大量に出る | Unity のバージョンが違う。README に書かれたバージョンで開き直す |

---

## 9. 関連ドキュメント

- [作品の公開手順](RELEASE_GUIDE.md)（Releases と unityroom で公開する）
- [引き継ぎ書](HANDOVER.md)（org の運用ルール：Owner・命名規則・年間スケジュール）
