# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

task-board は、React + Vite で作られたシンプルなタスク管理（ToDo）アプリ。
タスクの追加・完了切り替え・削除ができ、状態は `localStorage` に保存されてリロードしても消えない。

## コマンド

- `npm install` — 依存関係のインストール
- `npm run dev` — 開発サーバー起動（Vite）
- `npm run build` — 本番ビルド（`dist/` に出力）
- `npm run preview` — ビルド済みアプリのプレビュー
- `npm run lint` — oxlint によるLint

このプロジェクトに自動テストはまだ存在しない。

## デプロイ先

- https://ユーザー名.github.io/task-board/ （実際のURLは https://tkotsuka2004-ops.github.io/task-board/ ）
- `main` ブランチへの push をトリガーに `.github/workflows/deploy-pages.yml` が GitHub Actions 上でビルドし、GitHub Pages へ自動デプロイする。
- `vite.config.js` の `base: '/task-board/'` はこの GitHub Pages のパスに合わせているため、リポジトリ名を変更する場合はここも合わせて変更すること。

## 技術スタック

- React 19（関数コンポーネント + Hooks のみ。クラスコンポーネントは使わない）
- Vite 8（ビルドツール / 開発サーバー）
- oxlint（Lint。ESLintではない）
- プレーンCSS（CSS Modulesやスタイリングライブラリは未導入。コンポーネントごとに対応する `.css` ファイルを直接importする）
- 状態管理はReact標準の `useState` / `useEffect` のみ（Redux等の外部ライブラリは未導入）
- 永続化は `localStorage`（バックエンド/DBは無し）

## コンポーネント・命名規約

- コンポーネントファイルは `PascalCase.jsx`（例: `App.jsx`）とし、対応するスタイルは同名の `PascalCase.css` に置く。
- コンポーネント内のイベントハンドラ・ロジック関数は動詞始まりの `camelCase`（例: `addTask`, `toggleTask`, `deleteTask`）。
- CSS クラス名は `kebab-case`（例: `task-board`, `task-form`, `task-list`, `delete-button`）。状態を表すクラスは `task done` のように基底クラスに状態クラスを併記する形にする。
- localStorage のキーは `task-board.<用途>` の形式（例: `task-board.tasks`）で名前空間を分ける。

## Git運用ルール

- **コードに変更を加えるたびに、コミットを作成し GitHub にプッシュする。** 変更を溜め込まず、意味のあるまとまりができた時点で都度 commit → push を行うこと。
- コミットメッセージは「何を」ではなく「なぜ」変更したのかが伝わるように簡潔に書く。
- force push や履歴の書き換え（rebase -i, reset --hard など）は行わない。
- push 前に `git status` で意図しないファイル（機密情報や不要なビルド成果物など）が含まれていないか確認する。
