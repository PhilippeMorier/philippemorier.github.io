---
title: GIT
definition: Open source distributed version control system.
tags: git vcs
---

- [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Add auto-completion in bash](https://git-scm.com/book/en/v2/Appendix-A:-Git-in-Other-Environments-Git-in-Bash)
  - [git-completion.bash](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
  - On most Linux distributions it is already installed but maybe broken, if so
    run:  
    `sudo apt-get install git-core bash-completion`
- Add branch name to shell
  - [git-prompt.sh](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh)
  - .bashrc
    ```
    # GIT prompt
    . ~/Projects/git-prompt.sh
    export GIT_PS1_SHOWDIRTYSTATE=1
    export PS1='\[\e[1;32m\]\u\[\e[m\]@\[\e[33m\]\h\[\e[m\]:\[\e[34m\]\w\[\e[m\]$(__git_ps1 " (%s)")\$ '
    ```
  - http://ezprompt.net/
- [GIT Aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)
  ```bash
  git config --global alias.co checkout
  git config --global alias.br branch
  git config --global alias.ci commit
  git config --global alias.st status
  git config --global alias.sr "log --all --oneline -S"
  ```
- [GIT rerere](https://git-scm.com/docs/git-rerere) (*Re*use *re*corded
  *re*solution of conflicted merges)
- [GIT push --force-with-lease](https://git-scm.com/docs/git-push#Documentation/git-push.txt---no-force-with-lease)
- [GIT rebase --interactive](https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---interactive)
- [Pro Git](https://git-scm.com/book/en/v2) (book)
