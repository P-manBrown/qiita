---
title: エイリアスの設定方法【bash】【zsh】
tags:
  - Bash
  - Zsh
  - bashrc
  - zshrc
  - 初学者
private: false
updated_at: '2022-07-20T06:14:19+09:00'
id: 22e9a29c9e3ca7ed5cfa
organization_url_name: null
slide: false
ignorePublish: false
---
## エイリアスの設定方法
`alias 別名= '実際に実行するコマンド'`と.zshrc`や`.bashrc`に記述することでエイリアスが設定できます。

```.zshrc:エイリアス設定例
alias g='git'
alias gst='git status'
alias gd='git diff'
alias gdc='git diff --cached'
alias gl='git pull'
alias gup='git pull --rebase'
alias gp='git push'
alias gd='git diff'

alias d=‘docker’
alias dc=‘docker-compose’
alias dcnt=‘docker container’
alias dcur=‘docker container ls -f status=running -l -q’
alias dexec=‘docker container exec -it $(dcur)’
alias dimg=‘docker image’
alias drun=‘docker container run —rm -d’
alias drunit=‘docker container run —rm -it’
alias dstop=‘docker container stop $(dcur)’

```


