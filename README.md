cmd-shortcuts
=============

> git and other useful shortcuts to use in terminal

## .profile

    # general
    alias gs='git status '
    alias ga='git add '
    alias gb='git branch '
    alias gc='git commit'
    alias gca='git commit -a'
    alias gd='git diff'
    alias gco='git checkout '
    #alias gk='gitk --all&'
    #alias gx='gitx --all'
    
    # ham-handed
    alias got='git '
    alias get='git '
    
    # custom
    alias glog="git log --graph --pretty=format:'%Cred%h%Creset %an: %s - %Creset %C(yellow)%d%Creset %Cgreen(%cr)%Creset' --abbrev-commit --date=relative"
    alias gup='git stash && git fetch -p && git pull --rebase --progress && git stash pop'
    alias gpu='git stash && git fetch -p && git pull --rebase --progress && git stash pop'
    alias gp='git pull --rebase'
    alias pop='git stash pop'
    alias greb='git fetch -p && git pull --rebase '
    alias grebm='git fetch -p && git pull --rebase origin master'
    alias gf='git fetch -p'
    alias gcm='git commit -am '
    alias gph='git push origin HEAD'
    alias gphu='git push -u origin HEAD'
    alias gpo='git push origin '
    alias gbc=branchCreateCheckout
    alias gcmp=commitMessagePush
    
    function branchCreateCheckout {
    	git branch $1
    	git checkout $1
    }
    
    function commitMessagePush {
    	git commit -am $1
    	git push origin HEAD
    }
