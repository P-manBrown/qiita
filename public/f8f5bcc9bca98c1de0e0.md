---
title: 【GitHub】Issueテンプレートを作成する方法
tags:
  - GitHub
private: false
updated_at: '2024-07-10T23:54:54+09:00'
id: f8f5bcc9bca98c1de0e0
organization_url_name: null
slide: false
ignorePublish: false
---
## ファイルを作成する

以下のいずれかのファイルを作成します。

- `issue_template.md`
- `docs/issue_template.md`
- `.github/issue_template.md`
- `.github/ISSUE_TEMPLATE/issue_template.md`（ファイル名は任意）
- `docs/ISSUE_TEMPLATE/issue_template.md`（ファイル名は任意）

## 内容を記述する

```markdown:issue_template.md
---
name: Bug Report
about: Create a report to help us improve
title: '[BUG]: '
labels: bug
assignees: sample

---

## Summary
<!-- このIssueの目的と概要を簡潔に記述してください -->

## Details
<!-- 問題の詳細やIssueに対する具体的な要求を記述してください -->

## Steps to Reproduce
<!-- 問題の再現手順を記述してください -->
1. 
2. 
3. 

## Expected Behavior
<!-- 期待される挙動について記述してください -->

## Actual Behavior
<!-- 実際に発生した挙動について記述してください -->

## Screenshots
<!-- 問題を示すスクリーンショットがあれば添付してください -->

## Environment
<!-- 問題が発生した環境（OS、ブラウザ、バージョンなど）について記述してください -->

## Additional Context
<!-- その他、特記事項があれば記述してください -->

```

## 参考

https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/manually-creating-a-single-issue-template-for-your-repository
