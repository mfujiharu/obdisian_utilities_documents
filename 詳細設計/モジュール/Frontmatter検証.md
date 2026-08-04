---
title: Frontmatter検証
type: タスク
description: Frontmatterの必須項目、型、許容値、配置整合性の検証仕様を定める。
created: 2026-08-04T14:05:44+09:00
updated: 2026-08-04T14:06:40+09:00
---
# 対象モジュール
- `frontmatter_validator.py`
# 検証対象
- 必須フィールドの存在と非空
- 型、許容値、日時書式
- type別の条件付き必須項目
- フォルダ配置、`project_link`、フィールド間の整合性
# インターフェース
- `validate_common(path, frontmatter)`
- `validate_project_note(path, frontmatter)`
- `validate_note(path, frontmatter, project_context)`
# 重大度
## ERROR
必須欠落、空値、型不正、許容値外、日時不正、配置矛盾、リンク矛盾、対象を一意に特定できない状態。
## WARNING
推奨項目不足、結果へ影響しない任意項目の不整合、安全に既存書式を踏襲できる差異。
## INFO
省略可能項目への既定値適用、抽出条件不一致、正常な対象外判定。
# 中断単位
- 管理ノートERROR：プロジェクト単位
- 読み取り対象ERROR：原則ノート単位
- 書き込み対象ERROR：書き込み中止
- 転記先ERROR：追記と転記済みマーキングの両方を行わない
- 複数ファイル整合性が確保できない：プロジェクトまたはタスク単位
# 既定値
未定義と空値を区別する。仕様で既定値がある任意項目の未定義は、Frontmatter自体を更新せず評価時だけ既定値を使用する。空値はERRORとする。
# 検証条件の正本
意味と許容値はデータ整理ルールを正とする。初期実装はPython内のスキーマとし、将来`config/schemas/`へ外部化する。
