# Daily Report Repository

このリポジトリは学習記録を管理するためのものです。日々の学習内容を Markdown 形式で保存し、GitHub Actions を利用して月報・週報を自動生成します。

## 日報の書き方
- `YYYY/MM/DD.md` の形式で `2024/`, `2025/` ディレクトリ以下に作成します。
- Markdown でその日の学習内容を記録してください。

## 月報・週報生成ワークフロー
- `.github/workflows/generate_monthly_report.yml`
  日報を結合してから Gemini API を利用し月報 (`monthly_report/`) を作成します。
- `.github/workflows/generate_weekly_report.yml`
  指定週の学習内容を要約し `weekly_report/` に出力します。
- これらのワークフローは **workflow_dispatch** で手動実行します。必要に応じて `schedule` トリガーを追加することも可能です。
  実行後、ログに生成されたレポートへの URL が表示されます。
- 例えば `schedule` を使う場合:
```yaml
on:
  schedule:
    - cron: "0 0 1 * *"
```
- API 呼び出しには `GEMINI_API_KEY`、GitHub への push には `GITHUB_TOKEN` が利用されます。Secrets に設定してください。

## ディレクトリ構成
- `2024/`, `2025/` : 年ごとの日報を月別に格納
- `monthly_report/` : 月報を保存
- `weekly_report/` : 週報を保存

## 使い方の例
1. 毎日 `202X/MM/DD.md` を追加・コミットします。
2. `Generate Monthly Report` ワークフローを実行して月報を生成します。
3. 必要に応じて `Generate Weekly Report` を実行します。

