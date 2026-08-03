---
title: Python実行・AIエージェント情報
type: タスク
description: PythonによるAIを用いた処理の前提となる、Python実行環境およびAIエージェント（Antigravity）へのアクセス情報についてまとめる。
created: 2026-07-30
updated: 2026-08-03
---
# 目的
PythonによるAIを用いた処理の前提となる、Python実行環境の情報をまとめる。
またAIエージェントにアクセスするための基本情報も記載する。
# Python動作環境
## 実行環境
- OS： Windows11
- Python: 3.x
- 仮想環境： venv

仮想環境の作成： `python -m venv .venv --copies`
## Pythonライブラリ (`requirements.txt`)

```
# HTTP API通信（Antigravity API等）
requests>=2.32.0

# Obsidian MarkdownのYAML Frontmatter解析
python-frontmatter>=1.1.0

# YAML処理
PyYAML>=6.0.0

# Markdown解析
markdown-it-py>=3.0.0

# Markdown整形・書き戻し（インデント構造を保ったまま出力）
mdformat>=0.7.0

# mdformatでフロントマター(YAML)を保持するプラグイン
mdformat-frontmatter>=2.0.0

# Markdown拡張解析用
mdit-py-plugins>=0.4.0

# 日付・時刻処理
python-dateutil>=2.9.0

# 環境変数管理（APIキー等）
python-dotenv>=1.0.0
```

# Obsidianコミュニティプラグイン
Pythonスクリプトとは別に、一部タスクはObsidianのコミュニティプラグインに依存する。
## Gemini Scribe
Obsidianのチャットから、ノートを`@`参照しつつGeminiと対話できるコミュニティプラグイン。
Pythonスクリプトとは独立した経路であり、本システムのAI問い合わせ運用ルール（呼び出し粒度・JSON出力形式・キャッシュ等）の対象外（ユーザーによる対話的な利用のため）。
# フォルダ構造
- `Vault/`
    - `Utilities/`
        - `config/`
            - `.env` (APIキー、トークン情報)
            - `config.yaml` (共通設定：vault, ai, run, logging, backup, markdown_format等)
            - `project_types/`
                - `プロジェクトタイプ名.yaml`（`project_type`ごとの規約値。ファイル名はモジュールと同じ`project_type_mapping`マッピングで解決する）
            - `tasks/`
                - `個別タスク名.yaml`（タスク別設定）
        - `Python/`
            - `.venv/`
            - `taskscripts/`
                - `個別タスク名.py` (タスクごとの処理)
            - `modules/`
                - `モジュール.py` （汎用モジュール）
                - `project_types/`
                    - `プロジェクトタイプ名.py`（各project_type固有のモジュール。ファイル名は半角英数とし、`config.yaml`の`project_type_mapping`で日本語のproject_typeと対応付ける）
            - `snapshots/`（編集前のスナップショット保存領域）
            - `logs/` (実行ログ保存領域）
            - `cache/` (一次キャッシュ保存領域)
            - `prompts/`（プロンプトテンプレート置き場）
            - `main.py` (タスク自動ロード・実行起点)
            - `requirements.txt`
        - `Powershell/`
            - `PSスクリプト名.ps1` (タスクスケジューラに登録するPowershell）
# AIエージェント
Antigravity エージェントを利用する。
アクセスするためのAntigravity APIキーの詳細は、[[Utilities/Documents/詳細設計/共通設定・モジュール仕様#.env|共通設定・モジュール仕様]]を参照せよ。
# 設定ファイル
Pythonの各種設定は、[[Utilities/Documents/詳細設計/共通設定・モジュール仕様#設定ファイル（`config/`以下）|共通設定・モジュール仕様]]を参照せよ。
