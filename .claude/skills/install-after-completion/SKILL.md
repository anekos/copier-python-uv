---
name: install-after-completion
description: Use after finishing implementation, bugfix, or refactoring work on this project (before reporting completion to the user), to install the updated binary via `make install` so the user can run the new version immediately.
---

# Install After Completion

## Overview

このプロジェクト ({{ project_name }}) は `uv tool install` でユーザー環境にインストールされた CLI として使われる。コード変更しただけではユーザーが実行する `{{ package_name }}` バイナリは古いままなので、作業完了を宣言する前に必ず `make install` を実行してインストール済みバイナリを更新する。

## When to Use

以下に該当する作業を完了した直後、ユーザーへ完了報告する**前**に実行する:

- `src/` 配下の Python コードを変更した
- `pyproject.toml` の依存関係やエントリポイントを変更した
- バグ修正、機能追加、リファクタリングを行った

## When NOT to Use

- ドキュメントのみの変更 (README.md など)
- `.claude/` 配下の設定変更のみ
- テストやチェック (`make check` / `make test`) のみの実行
- ユーザーがインストールを明示的に拒否している場合

## How to Run

```bash
make install
```

これは内部的に `uv tool install --force --reinstall .` を実行する。

実行後に完了報告すること。失敗した場合はインストールエラーを修正してから完了とする (バイナリが古いまま完了宣言しない)。

## Quick Reference

| 状況 | 実行する? |
|------|----------|
| `src/{{ package_name }}/*.py` を編集した | はい |
| `pyproject.toml` の `[project.scripts]` を変更 | はい |
| `Makefile` を変更 | はい (install ターゲットに影響しうる) |
| README.md のみ変更 | いいえ |
| 確認のため `make check` を流しただけ | いいえ |