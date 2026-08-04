---
title: ノート探索・Wikilink構築
type: タスク
description: プロジェクト探索およびWikilink生成の共通仕様を定める。
created: 2026-08-04T14:05:44+09:00
updated: 2026-08-04T14:06:42+09:00
---
# 対象モジュール
- `project_discovery.py`
- `wikilink.py`
# `project_discovery.py`
## `find_projects(project_type, status=True, ai_check=True)`
1. Vault直下のプロジェクト候補を走査する。
2. フォルダ名と同名で`type: プロジェクト管理ノート`のノートを取得する。
3. Frontmatterを検証する。
4. 引数条件と一致するプロジェクトを抽出する。
5. `project_name`、プロジェクトフォルダ、管理ノートのパスを返す。
`ai_check: false`のプロジェクトでは、対象外判定後に本文走査、AI入力、更新、結合成果物への収録を行わない。
# `wikilink.py`
`config.yaml`の`markdown_format.wikilink_style`に従ってWikilinkを生成する。
## `full_path_no_ext`
Vaultルートからの相対パスから`.md`を除く。
```markdown
[[今世は悪女/Settings/シルヴィア]]
```
パス区切りはOSにかかわらず`/`へ統一する。
