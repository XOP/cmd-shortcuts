cmd-shortcuts
=============

> git and other useful shortcuts to use in terminal

## .profile

```sh

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
	git commit -am "$1"
	git push origin HEAD
}

```

## .bashrc

```sh

# auto-add ssh-agent

# Note: ~/.ssh/environment should not be used, as it
#       already has a different purpose in SSH.

env=$HOME/.ssh/environment

# Note: Don't bother checking SSH_AGENT_PID. It's not used
#       by SSH itself, and it might even be incorrect
#       (for example, when using agent-forwarding over SSH).

agent_is_running() {
    if [ "$SSH_AUTH_SOCK" ]; then
        # ssh-add returns:
        #   0 = agent running, has keys
        #   1 = agent running, no keys
        #   2 = agent not running
        ssh-add -l >/dev/null 2>&1 || [ $? -eq 1 ]
    else
        false
    fi
}

agent_has_keys() {
    ssh-add -l >/dev/null 2>&1
}

agent_load_env() {
    . "$env" >/dev/null
}

agent_start() {
    (umask 077; ssh-agent >"$env")
    . "$env" >/dev/null
}

if ! agent_is_running; then
    agent_load_env
fi

# if your keys are not stored in ~/.ssh/id_rsa.pub or ~/.ssh/id_dsa.pub, you'll need
# to paste the proper path after ssh-add
if ! agent_is_running; then
    agent_start
    ssh-add
elif ! agent_has_keys; then
    ssh-add
fi

unset env


# aliases

function addSshAgent {
    eval $(ssh-agent -s)
    ssh-add ~/.ssh/id_rsa
}

alias agent=addSshAgent
```
