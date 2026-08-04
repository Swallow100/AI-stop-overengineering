# GPT-5.6 Stop Overengineering

GPT-5.6の過剰な実装やテストを抑えるためのAgent Skillです。

依頼された範囲を固定し、必要な変更と検証が終わった時点で作業を止めます。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 何を止めるのか

- 2行の修正を新しいフレームワークへ発展させる
- 将来使うかもしれない抽象化や依存関係を追加する
- 成功済みの同じテストを理由なく繰り返す
- レビューで見つけた隣接問題まで勝手に修正する
- 完了条件を満たした後も磨き続ける

「オーバーエンジニアリングしないで」だけでは曖昧です。このスキルは具体的な停止条件をエージェントへ渡します。

1. 依頼された成果と範囲を固定する。制約と必要な証拠も先に決める
2. 最も狭い責任範囲へ必要な変更だけを加える
3. 変更のリスクに応じてテスト量を決める
4. 今回直す問題と別件として報告する問題を分ける
5. 成功が証明された時点で作業を止める

## インストール

GitHub CLIがAgent Skillsに対応している場合：

```sh
gh skill install Swallow100/gpt-5-6-stop-overengineering gpt-5-6-stop-overengineering
```

手動の場合は [`skills/gpt-5-6-stop-overengineering`](skills/gpt-5-6-stop-overengineering) を利用するエージェントのskillsディレクトリへコピーしてください。

```text
.agents/skills/gpt-5-6-stop-overengineering/
.github/skills/gpt-5-6-stop-overengineering/
.claude/skills/gpt-5-6-stop-overengineering/
```

## 使い方

```text
Use $gpt-5-6-stop-overengineering to fix the mobile menu regression. Do not redesign the header.
```

日本語でも構いません。

```text
$gpt-5-6-stop-overengineering を使ってログイン画面のクラッシュだけ直して。認証設計の変更はしないで。
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

**このスキルを使う場合**

```text
null titleのクラッシュを直す
→ クラッシュを再現
→ 既存のtitle境界だけ修正
→ 関連する回帰テストだけ実行
→ 結果を報告して終了
```

## 安全性と位置づけ

このスキルは品質を下げるものではありません。セキュリティやデータ整合性に関わる変更では必要な広範囲テストを維持します。マイグレーションや公開API、リリースも同様です。ユーザーやリポジトリが指定した必須チェックは省略しません。

実行スクリプトやフックは含みません。ネットワーク通信やツール権限もありません。内容は単一の `SKILL.md` とUIメタデータだけです。

これは独立したコミュニティプロジェクトです。OpenAIその他のモデル提供者による公式プロジェクトではありません。非公開プロンプトは複製しません。特定モデルの挙動も断定しません。

---

## English

### GPT-5.6 Stop Overengineering

**Stop GPT-5.6 from turning a two-line fix into a framework.**

GPT-5.6 Stop Overengineering is a tiny, model-agnostic Agent Skill for controlling scope creep, test loops, speculative abstractions, and unrequested polish in GPT-5.6 and other coding agents.

> Smallest sufficient change. Proportionate proof. Then stop.

### The policy

1. Lock the requested outcome, scope, constraints, and proof.
2. Make the smallest sufficient change at the narrowest ownership boundary.
3. Match verification effort to actual risk.
4. Separate in-scope blockers from adjacent improvements.
5. Stop when the outcome is proven.

### Install

```sh
gh skill install Swallow100/gpt-5-6-stop-overengineering gpt-5-6-stop-overengineering
```

For manual installation, copy [`skills/gpt-5-6-stop-overengineering`](skills/gpt-5-6-stop-overengineering) into a skills directory supported by your agent.

### Use

```text
Use $gpt-5-6-stop-overengineering to fix the null title crash. Do not redesign the content model.
```

### What it will not do

This skill does not lower the bar for security, data integrity, public API changes, migrations, or releases. It preserves explicit acceptance criteria and mandatory repository checks. If the user asks for an exhaustive audit or broad refactor, that broader scope remains authoritative.

The skill uses the open `SKILL.md` format and has no runtime dependencies, scripts, hooks, network calls, or tool permissions. It is designed for Codex, Claude Code, GitHub Copilot, and other Agent Skills-compatible tools.

This is an independent community project. It is not affiliated with or endorsed by OpenAI, Anthropic, GitHub, Microsoft, or any model provider. It does not reproduce proprietary prompts or claim that a named model always behaves in a particular way.

### Contributing

Small, evidence-backed improvements are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md). Please solve observed failure modes without turning the skill into a general software-engineering handbook.

### License

MIT. See [LICENSE](LICENSE).
