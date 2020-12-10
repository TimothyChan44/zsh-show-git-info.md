# zsh-show-git-info.md

tag1: zsh
tag2: git branch
tag3: $PS1
```
# vim ~/.zshrc


# turn on colorful mode:
autoload -U colors && colors;
function m32(){
    echo "\e[01;32m";
}
function m36(){
    echo "\e[01;36m";
}
function m0(){
    echo "\e[0m";
}
# show git branch info
function git_branch() {
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
PS1="%n@%m \$(m36)%1~\$(m0) \$(m32)\$(_git_branch_name)\$(_git_is_dirty)\$(m0) \$ ";
setopt prompt_subst;
```
