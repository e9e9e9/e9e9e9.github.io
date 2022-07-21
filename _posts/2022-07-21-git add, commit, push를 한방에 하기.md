---
title: "git add, commit, push를 한방에 하기"
categories: git
tags: [git, git add, git commit, git push]
comments: true
toc: true
author_profile: true
sidebar:
  nav: "docs"
---
## Motivation

 github.io를 사용해 보니 내용 수정 및 업데이트가 너무 잦아진다. 업데이트 반영을 위해 git add, git commit, git push의 작업을 반복해서 하는 것이 너무 불편하다. 

 shell prompt에서 alias를 설정하여 쉽게 문제를 해결해 보자

---

## alias 설정

**파일 수정**

```bash
vi ~/.zshrc
```

**alias 추가**

```bash
alias git_acp='git status && git add --all && git commit -m "new" && git push origin main'
```

alias 적용

```bash
. ~/.zshrctes
```

---

## 실행

```bash
git_acp
```
{% include video id="77Kj83nsshE" provider="youtube" %}