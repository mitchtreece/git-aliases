# Git Aliases

You should add aliases via git's 'config --global alias.<aliasname> <command>' command line syntax. <br>
However, if you must add them manually the config file is located at '~/.gitconfig'

**Status**<br>
s = status

**Pretty log**<br>
lg = log --graph --pretty=format:'%Cred%h%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative

**Checkout**<br>
co = checkout

**Branches**<br>
b = branch -vv <br>
ba = branch -vv --all <br>
rmbranch = branch -d <br>
mkbranch = checkout -b <br>
search = "!f() { git branch -ra | grep $1; }; f" <br>

**Local**<br>
ca = "!f() { git add --all && git commit -m '$1'; }; f" <br>
pullall = !git pull && git submodule update --init --recursive <br>
ammend = commit --all --ammend -C HEAD <br>
nuke = reset --hard HEAD <br>

**Merges**<br>
hopmerge = "!f() { local source_branch=$(git rev-parse --abbrev-ref HEAD); git co ${1-dev}; git fetch; git pullall; git co $source_branch; git pullall; git merge ${1-dev}; }; f"

_hopmerge_ merges a specified (defaults to "dev") branch into the current working branch. This pulls and recursively updates submodules as well. (ex. git hopmerge my-branch)
