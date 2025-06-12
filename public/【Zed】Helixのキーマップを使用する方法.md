---
title: 【Zed】Helixのキーマップを使用する方法
tags:
  - zed-editor
private: false
updated_at: '2025-06-12T20:45:52+09:00'
id: c7b956c3a3ba8419f457
organization_url_name: null
slide: false
ignorePublish: false
---

## Helixのキーマップを使用する方法

`settings.json`に以下の記述を追加することでノーマルモードでHelixのキーマップが使用できるようになります。

```json
{
	"vim": {
    "default_mode": "helix_normal"
  },
}
```

![screen-recording-64.gif](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2342443/08be8198-a92d-4818-b57d-4891096de24f.gif)

## デフォルトのキーマップ

デフォルトのキーマップは以下のとおりです。

```json
  {
    "context": "vim_mode == helix_normal && !menu",
    "bindings": {
      "escape": "editor::Cancel",
      "ctrl-[": "editor::Cancel",
      ":": "command_palette::Toggle",
      "shift-d": "vim::DeleteToEndOfLine",
      "shift-j": "vim::JoinLines",
      "y": "editor::Copy",
      "shift-y": "vim::YankLine",
      "i": "vim::InsertBefore",
      "shift-i": "vim::InsertFirstNonWhitespace",
      "a": "vim::InsertAfter",
      "shift-a": "vim::InsertEndOfLine",
      "o": "vim::InsertLineBelow",
      "shift-o": "vim::InsertLineAbove",
      "~": "vim::ChangeCase",
      "ctrl-a": "vim::Increment",
      "ctrl-x": "vim::Decrement",
      "p": "vim::Paste",
      "shift-p": ["vim::Paste", { "before": true }],
      "u": "vim::Undo",
      "ctrl-r": "vim::Redo",
      "r": "vim::PushReplace",
      "s": "vim::Substitute",
      "shift-s": "vim::SubstituteLine",
      ">": "vim::Indent",
      "<": "vim::Outdent",
      "=": "vim::AutoIndent",
      "g u": "vim::PushLowercase",
      "g shift-u": "vim::PushUppercase",
      "g ~": "vim::PushOppositeCase",
      "\"": "vim::PushRegister",
      "g q": "vim::PushRewrap",
      "g w": "vim::PushRewrap",
      "ctrl-pagedown": "pane::ActivateNextItem",
      "ctrl-pageup": "pane::ActivatePreviousItem",
      "insert": "vim::InsertBefore",
      // tree-sitter related commands
      "[ x": "editor::SelectLargerSyntaxNode",
      "] x": "editor::SelectSmallerSyntaxNode",
      "] d": "editor::GoToDiagnostic",
      "[ d": "editor::GoToPreviousDiagnostic",
      "] c": "editor::GoToHunk",
      "[ c": "editor::GoToPreviousHunk",
      // Goto mode
      "g n": "pane::ActivateNextItem",
      "g p": "pane::ActivatePreviousItem",
      // "tab": "pane::ActivateNextItem",
      // "shift-tab": "pane::ActivatePrevItem",
      "shift-h": "pane::ActivatePreviousItem",
      "shift-l": "pane::ActivateNextItem",
      "g l": "vim::EndOfLine",
      "g h": "vim::StartOfLine",
      "g s": "vim::FirstNonWhitespace", // "g s" default behavior is "space s"
      "g e": "vim::EndOfDocument",
      "g y": "editor::GoToTypeDefinition",
      "g r": "editor::FindAllReferences", // zed specific
      "g t": "vim::WindowTop",
      "g c": "vim::WindowMiddle",
      "g b": "vim::WindowBottom",

      "x": "editor::SelectLine",
      "shift-x": "editor::SelectLine",
      // Window mode
      "space w h": "workspace::ActivatePaneLeft",
      "space w l": "workspace::ActivatePaneRight",
      "space w k": "workspace::ActivatePaneUp",
      "space w j": "workspace::ActivatePaneDown",
      "space w q": "pane::CloseActiveItem",
      "space w s": "pane::SplitRight",
      "space w r": "pane::SplitRight",
      "space w v": "pane::SplitDown",
      "space w d": "pane::SplitDown",
      // Space mode
      "space f": "file_finder::Toggle",
      "space k": "editor::Hover",
      "space s": "outline::Toggle",
      "space shift-s": "project_symbols::Toggle",
      "space d": "editor::GoToDiagnostic",
      "space r": "editor::Rename",
      "space a": "editor::ToggleCodeActions",
      "space h": "editor::SelectAllMatches",
      "space c": "editor::ToggleComments",
      "space y": "editor::Copy",
      "space p": "editor::Paste",
      // Match mode
      "m m": "vim::Matching",
      "m i w": ["workspace::SendKeystrokes", "v i w"],
      "shift-u": "editor::Redo",
      "ctrl-c": "editor::ToggleComments",
      "d": "vim::HelixDelete",
      "c": "vim::Substitute",
      "shift-c": "editor::AddSelectionBelow"
    }
  },

```

