# Git Aliases

#### You should add aliases via git's 'config --global alias.<aliasname> <command>' command line syntax.
#### However, if you must add them manually the config file is located at '~/.gitconfig'.

s = status  
lg = log --graph --pretty=format:'%Cred%h%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative  
co = checkout  
rmbranch = branch -d  
mkbranch = checkout -b  
b = branch -vv  
ba = branch -vv --all  
