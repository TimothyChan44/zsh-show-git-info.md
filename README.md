# zsh-show-git-info.md

tag1: zsh

tag2: git branch

tag3: $PS1

```
# vim ~/.zshrc


# turn on colorful mode:
autoload -U colors && colors;
### cyan-blue
function m32(){
    echo "\e[01;32m";
}
### green
function m36(){
    echo "\e[01;36m";
}
### white
function m0(){
    echo "\e[0m";
}
# show git branch info
function _git_branch_name() {
   branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
   if [ "${branch}" != "" ];then
       if [ "${branch}" = "(no branch)" ];then
           branch="(`git rev-parse --short HEAD`...)"
       fi
       echo "(${branch})";
   fi
}
# you may be wanna to show _git_is_dirty
function _git_is_dirty() {
  git diff --quiet 2> /dev/null || echo '*'
}
autoload -U promptinit && promptinit;
cd /Users/game-netease/Documents/win-workspace/gdlcdn
PROMPT="%n@%m %{$fg[cyan]%}%1~%{$fg[white]%} %{$fg[green]%}\$(_git_branch_name)\$(_git_is_dirty)%{$fg[white]%} \$ ";
RPROMPT="[%{$fg[yellow]%}%?%{$reset_color%}]"
setopt prompt_subst;
```
