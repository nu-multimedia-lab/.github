<!--
  このリポジトリは unity-game-template から作られています。
  - Unity プロジェクトは、このリポジトリの直下（Assets/ と ProjectSettings/ がここに来る位置）に作ってください。
    サブフォルダに作ると .gitignore と自動ビルドが効きません。
  - この README の（ ）の部分を書き換え、不要な項目は消してOK。
-->

# （ゲームタイトル）

![スクリーンショット](docs/screenshot.png)
<!-- docs/ フォルダにスクショを置く。GIF だとなお良い -->

（どんなゲームか 1〜2 行で。例：2D 横スクロールのアクションゲーム。迫ってくる団子を斬りながら進む）

## 遊ぶ

- ブラウザで遊ぶ：[unityroom](https://unityroom.com/games/（ゲームID）)
- ダウンロード（Windows）：[Releases](../../releases/latest)

## 操作方法

| 操作 | キーボード | ゲームパッド |
|---|---|---|
| 移動 | WASD / 矢印キー | 左スティック |
| ジャンプ | Space | A |
| 攻撃 | J | X |
| ポーズ | Esc | Start |

## 概要

| 項目 | 内容 |
|---|---|
| ジャンル | （アクション / パズル / ...） |
| 制作 | （2026 夏ゲームジャム A チーム） |
| 制作期間 | （2026-08-01 〜 2026-08-14） |
| エンジン | Unity （6000.x.xx） |
| 対応環境 | Windows / ブラウザ（WebGL） |

## メンバー

| 名前 | 担当 |
|---|---|
| （ハンドルネーム） | リーダー・プログラム |
| （ハンドルネーム） | グラフィック |
| （ハンドルネーム） | サウンド |

## 使用素材・クレジット

<!-- 使った素材は全部書く。公開前チェックで必要になる -->

| 種類 | 素材名 | 作者 / 配布元 | ライセンス |
|---|---|---|---|
| フォント | Noto Sans JP | Google | SIL OFL 1.1 |
| BGM | （曲名） | （サイト名） | （利用規約URL） |
| 効果音 | （素材名） | （サイト名） | （利用規約URL） |

> Asset Store の有料アセットを使っている場合はここに明記し、**リポジトリを public にしないこと**。

## 開発者向け

### 環境

- Unity （6000.x.xx）※Unity Hub でこのバージョンを入れてから開く
- Git LFS（`git lfs install` を一度実行しておく）

### クローン

```bash
git lfs install
git clone https://github.com/nu-multimedia-lab/（リポジトリ名）.git
```

### ビルド・公開

`v1.0.0` のようなタグを push すると、GitHub Actions が Windows 版と WebGL 版をビルドし、Releases に zip で添付します。

```bash
git tag v1.0.0
git push origin v1.0.0
```

事前に Unity ライセンスの Secrets 登録が必要です。手順と、手動で公開する方法は [作品の公開手順](https://github.com/nu-multimedia-lab/.github/blob/main/docs/RELEASE_GUIDE.md) を参照。
