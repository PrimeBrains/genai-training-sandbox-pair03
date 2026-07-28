# genai-training-sandbox

生成AI新人研修（エンジニア職向け・半日）のハンズオン用サンドボックスです。  
小さな経費精算サービス（Java 21 / Spring Boot / Gradle）を題材に、**エージェント型 AI との開発**を体験します。

---

## この研修でやること

「生成AI = Web チャット」だと思っていませんか？

**Claude Code** のようなエージェント型 AI は、Issue を読み、ブランチを切り、コードを修正し、PR を出すところまで自走します。  
この研修では、そのサイクルをあなた自身の手で体験します。

- GitHub Issues に積まれたタスクを Claude Code に渡す
- Claude Code がブランチ作成・調査・実装・PR 作成を行う
- 人間はレビューとマージだけを担当する

---

## プロジェクト構成

```
genai-training-sandbox/
├── src/
│   ├── main/java/com/example/training/
│   │   ├── ExpenseService.java   # 経費精算サービス（精算ロジック）
│   │   └── ExpenseItem.java      # 経費明細モデル（費目・金額）
│   └── test/java/com/example/training/
│       └── ExpenseServiceTest.java  # 単体テスト
├── docs/
│   └── research/                 # 調査レポートの置き場
├── CLAUDE.md                     # Claude Code への作業ルール
└── build.gradle                  # Gradle ビルド設定
```

---

## 経費精算サービスの仕様

`ExpenseService` が実装する精算ルールは以下のとおりです。

| 費目 | ルール |
|------|--------|
| 交通費 (TRANSPORT) | 1明細あたり上限 **3,000 円**。超過分は支給しない |
| 食事代 (MEAL) | **半額支給**（1円未満切り捨て） |
| 宿泊費 (LODGING) | 1明細あたり上限 **10,000 円**。超過分は支給しない |
| その他 (OTHER) | **全額支給** |

仕様の正は `ExpenseService.java` の Javadoc とテストコードです。

---

## 事前セットアップ（研修当日までに）

詳しい手順は [docs/事前セットアップ案内.md](docs/事前セットアップ案内.md) を参照してください。  
対象は Windows PC、コマンドはすべて PowerShell で実行します。

### 1. 必要なツールをインストール

| ツール | インストール方法 |
|--------|----------------|
| JDK 21 | [Temurin 21](https://adoptium.net/) の .msi（「Add to PATH」を有効に） |
| Git for Windows | [git-scm.com](https://git-scm.com/) |
| GitHub CLI (gh) | [cli.github.com](https://cli.github.com/) |
| Claude Code | [claude.com/claude-code](https://claude.com/claude-code) |

### 2. GitHub 認証

```powershell
gh auth login
```

### 3. リポジトリのクローンと動作確認

```powershell
git clone <このリポジトリのURL>
cd genai-training-sandbox
.\gradlew.bat test
```

> `BUILD FAILED`（テスト失敗）まで進めばセットアップ成功です。テストが落ちているのは仕様です。当日はここから始めます。

---

## 研修の進め方

1. Claude Code を起動する
2. 「次にやるべきタスクを提案して」と話しかける
3. Claude Code が Issue を確認し、着手から PR 作成まで進める
4. あなたはレビューしてマージする

作業ルールは `CLAUDE.md` に書かれており、Claude Code はそれを読んで Issue 駆動で動きます。

---

## テスト実行

```powershell
.\gradlew.bat test
```

全件成功すると `BUILD SUCCESSFUL` と表示されます。

---

## 研修後も

このリポジトリは持ち帰り OK です。自由に Issue を追加して、Claude Code との開発を続けてみてください。
