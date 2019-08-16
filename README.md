# Git Aliases

You should add aliases via git's 'config --global alias.name {command}' syntax.<br>
However, if you must add them manually, the config file is located at `~/.gitconfig`

- s = status
- lg = log --graph --pretty=format:'%Cred%h%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
- co = checkout

- b = branch -vv
- ba = branch -vv --all
- mb = "!f() { git checkout -b $1 && git up; }; f"
- rb = "!f() { git branch -d $1 }; f"
- mkbranch = checkout -b
- rmbranch = branch -d

- search = "!f() { git branch -ra | grep $1; }; f"
- nuke = reset --hard HEAD

- pullall = !git pull && git submodule update --init --recursive
- ammend = commit --all --ammend -C HEAD
- ca = "!f() { git add --all && git commit -m '$1'; }; f"
- up = push -u origin HEAD # push & make local branch track remote
- down = !git pull && git submodule update --init --recursive # same as 'pullall'

- rmlf = "!f() { git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch $1' }; f" # remove large file
- fdiff = "!f() { git diff HEAD^ -- $1; }; f"

_**hopmerge**_ merges a specified (defaults to "dev") branch into the current working branch. This pulls and recursively updates submodules as well. (ex. git hopmerge my-branch)
- hopmerge = "!f() { local source_branch=$(git rev-parse --abbrev-ref HEAD); git co ${1-dev}; git fetch; git pullall; git co $source_branch; git pullall; git merge ${1-dev}; }; f"

_[Sweep](https://stackoverflow.com/questions/6127328/how-can-i-delete-all-git-branches-which-have-been-merged)_ cleans up local branches that have already been merged.
- sweep = !git branch --merged $([[ $1 != \"-f\" ]] \\\n&& git rev-parse master) | egrep -v \"(^\\*|^\\s*(master|dev)$)\" \\\n| xargs git branch -d
