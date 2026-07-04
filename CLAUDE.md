# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

task-board は現在初期段階のプロジェクトで、リポジトリ内にはまだコードが存在しません。
機能や構成が追加され次第、このファイルに以下の情報を追記・更新してください。

- ビルド / Lint / テストの実行コマンド（単体テストを1件だけ実行する方法を含む）
- 全体のアーキテクチャ（複数ファイルにまたがる設計判断や責務分担など)

## Git運用ルール

- **コードに変更を加えるたびに、コミットを作成し GitHub にプッシュする。** 変更を溜め込まず、意味のあるまとまりができた時点で都度 commit → push を行うこと。
- コミットメッセージは「何を」ではなく「なぜ」変更したのかが伝わるように簡潔に書く。
- force push や履歴の書き換え（rebase -i, reset --hard など）は行わない。
- push 前に `git status` で意図しないファイル（機密情報や不要なビルド成果物など）が含まれていないか確認する。
