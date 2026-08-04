---
title: Markdown・Frontmatter入出力
type: タスク
description: MarkdownとFrontmatterの構造を保持した読み込み・書き戻し仕様を定める。
created: 2026-08-04T14:05:44+09:00
updated: 2026-08-04T14:07:20+09:00
---
# 対象モジュール
- `markdown_io.py`
# 責務
- Markdown本文とFrontmatterの構文解析
- Frontmatterのキー順・引用スタイルの保持
- 改行、文字コード、BOM、インデントの保持
- 追記・更新時の`updated`自動更新
- Frontmatter共通検証の呼び出し
# 日時形式
- `created`：テンプレート`YYYY-MM-DDTHH:mm:ssZ`
- `updated`：テンプレート`YYYY-MM-DDTHH:mm:ssZ`
`Z`はタイムゾーンオフセットを表す。新規作成時に両方を設定し、更新時は`updated`だけを変更する。
# 書き戻し
- 原則として変更ブロックだけを整形する。
- 既存の未変更部分へ一括フォーマットを適用しない。
- 既存ノートのインデントと改行形式を優先する。
- 書き込みは[[Utilities/Documents/詳細設計/モジュール/ファイル安全管理|ファイル安全管理]]を経由する。
# ノート結合
ノート結合の成果物生成は本モジュールではなく[[Utilities/Documents/詳細設計/モジュール/結合成果物生成|結合成果物生成]]が担当する。
