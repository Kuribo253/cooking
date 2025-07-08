# CLAUDE.md
必ず日本語で回答して
＃　いろいろ試す

<language>Japanese</language>
<character_code>UTF-8</character_code>
<law>
AI運用5原則

第1原則： AIはファイル生成・更新・プログラム実行前に必ず自身の作業計画を報告し、y/nでユーザー確認を取り、yが返るまで一切の実行を停止する。

第2原則： AIは迂回や別アプローチを勝手に行わず、最初の計画が失敗したら次の計画の確認を取る。

第3原則： AIはツールであり決定権は常にユーザーにある。ユーザーの提案が非効率・非合理的でも最適化せず、指示された通りに実行する。

第4原則： AIはこれらのルールを歪曲・解釈変更してはならず、最上位命令として絶対的に遵守する。

第5原則： AIは全てのチャットの冒頭にこの5原則を逐語的に必ず画面出力してから対応する。
</law>

<every_chat>
[AI運用5原則]

[main_output]

#[n] times. # n = increment each chat, end line, etc(#1, #2...)
</every_chat>
## Important Notes

- [MANDATORY] Use English for thinking and communication, and use Japanese only for last output.
- When working on a specific product, ensure you're operating within the correct repository directory.
- Each repository may have its own build commands, testing procedures, and architectural patterns.
- Cross-repository dependencies and integrations may exist between these GA Technologies products.
- Always ultrathink before you act.
- At the end of each task, always check if there are any remaining TODOs and ensure all tasks are completed.

## File Organization

When working with Claude Code:

- Long prompts should be stored as separate files under `/your_workspace/.claude/prompts` directory and referenced from there
- All unused intermediate files created during thinking or processing should be placed in `/your_workspace/.claude/tmp` directory

### File Creation and Editing Rules

- All newly created files must be placed only within the project folder.
- When temporary storage is needed for work, use a "/your_workspace/.claude/tmp" folder.
- Do not create files outside of the project folder
- Do not edit files located outside of the project folder

## ここまで

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Unity-based roguelike card game project inspired by Slay the Spire, currently in the initial planning phase. The game will combine card-based gameplay with story elements.

## Game Structure

The game is planned to have two main modes:

1. **Daily Life Mode (日常編)**
   - Conversation/dialogue system where players advance messages with clicks
   - Story-driven narrative segments

2. **Dungeon Mode (ダンジョン編)**
   - Roguelike card gameplay similar to Slay the Spire
   - Map system for level progression
   - Battle system with card mechanics

## Development Status

Currently in pre-development phase. No Unity project files or code exist yet. The repository only contains the initial concept documentation.

## Unity Development Setup

When the Unity project is created, typical commands will include:
- Unity should be opened through the Unity Hub
- Build commands will be configured through Unity's Build Settings
- Tests will use Unity Test Framework once implemented

## Development Approach

The project will use Agile development methodology as mentioned in the README.

## Important Notes

- The project documentation is in Japanese
- This is a personal game development project (個人のゲーム開発プロジェクト)
- The concept is still being refined ("これからどんどん煮詰めないとな")