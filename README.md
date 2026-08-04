# GPT-5.6 Stop Overengineering

**GPT-5.6に、小さな修正を巨大な改修へ育てさせない。**

GPT-5.6 Solをはじめとする高性能コーディングエージェントは、頼んだ作業が終わった後も、追加のリファクタリング、抽象化、テスト、レビュー修正を続けることがあります。

Just Enoughは、その「やりすぎ」を止めるための小さなAgent Skillです。

> 必要十分な変更。リスクに見合う検証。終わったら止まる。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 何を止めるのか

- 2行の修正を新しいフレームワークへ発展させる
- 将来使うかもしれない抽象化や依存関係を追加する
- 成功済みの同じテストを理由なく繰り返す
- レビューで見つけた隣接問題まで勝手に修正する
- 完了条件を満たした後も磨き続ける

「オーバーエンジニアリングしないで」だけでは曖昧です。このスキルは、エージェントへ具体的な停止条件を渡します。

1. 依頼された成果、範囲、制約、必要な証拠を固定する
2. 最も狭い責任範囲へ、必要十分な変更だけを加える
3. 変更のリスクに応じてテスト量を決める
4. 今回直す問題と、別件として報告する問題を分ける
5. 成功が証明された時点で作業を止める

## インストール

GitHub CLIがAgent Skillsに対応している場合：

```sh
gh skill install Swallow100/just-enough just-enough
```

手動の場合は [`skills/just-enough`](skills/just-enough) を、利用するエージェントのskillsディレクトリへコピーしてください。

```text
.agents/skills/just-enough/
.github/skills/just-enough/
.claude/skills/just-enough/
```

## 使い方

```text
Use $just-enough to fix the mobile menu regression. Do not redesign the header.
```

日本語でも構いません。

```text
$just-enough を使ってログイン画面のクラッシュだけ直して。認証設計の変更はしないで。
```

## 変化の例

**停止ルールがない場合**

```text
null titleのクラッシュを直す
→ コンテンツモデルを再設計
→ 新しいバリデーション基盤を追加
→ 無関係な呼び出し元も移行
→ 全テストを3回実行
```

**Just Enoughを使う場合**

```text
null titleのクラッシュを直す
→ クラッシュを再現
→ 既存のtitle境界だけ修正
→ 関連する回帰テストだけ実行
→ 結果を報告して終了
```

## 安全性と位置づけ

このスキルは品質を下げるものではありません。セキュリティ、データ整合性、マイグレーション、公開API、リリースなどの高リスク変更では、必要な広範囲テストを維持します。ユーザーやリポジトリが指定した必須チェックも省略しません。

実行スクリプト、フック、ネットワーク通信、ツール権限は含まれていません。内容は単一の `SKILL.md` とUIメタデータだけです。

これは独立したコミュニティプロジェクトであり、OpenAIその他のモデル提供者による公式プロジェクトではありません。非公開プロンプトの複製や、特定モデルが常に同じ挙動をするという主張も行いません。

---

## English

### GPT-5.6 Stop Overengineering

**Stop GPT-5.6 from turning a two-line fix into a framework.**

Just Enough is a tiny, model-agnostic Agent Skill for controlling scope creep, test loops, speculative abstractions, and unrequested polish in GPT-5.6 and other coding agents.

> Smallest sufficient change. Proportionate proof. Then stop.

### The policy

1. Lock the requested outcome, scope, constraints, and proof.
2. Make the smallest sufficient change at the narrowest ownership boundary.
3. Match verification effort to actual risk.
4. Separate in-scope blockers from adjacent improvements.
5. Stop when the outcome is proven.

### Install

```sh
gh skill install Swallow100/just-enough just-enough
```

For manual installation, copy [`skills/just-enough`](skills/just-enough) into a skills directory supported by your agent.

### Use

```text
Use $just-enough to fix the null title crash. Do not redesign the content model.
```

### What it will not do

Just Enough does not lower the bar for security, data integrity, public API changes, migrations, or releases. It preserves explicit acceptance criteria and mandatory repository checks. If the user asks for an exhaustive audit or broad refactor, that broader scope remains authoritative.

The skill uses the open `SKILL.md` format and has no runtime dependencies, scripts, hooks, network calls, or tool permissions. It is designed for Codex, Claude Code, GitHub Copilot, and other Agent Skills-compatible tools.

This is an independent community project. It is not affiliated with or endorsed by OpenAI, Anthropic, GitHub, Microsoft, or any model provider. It does not reproduce proprietary prompts or claim that a named model always behaves in a particular way.

### Contributing

Small, evidence-backed improvements are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md). Please solve observed failure modes without turning the skill into a general software-engineering handbook.

### License

MIT. See [LICENSE](LICENSE).
