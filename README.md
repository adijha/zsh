ZSHRC config and aliases are in .zshrc file

## Here are some BASH FUNCTIONS for git
```
function gitpush() {
    git add .
    if [ "$1" != "" ]
    then
        git commit -m "$1"
    else
        print $fg_bold[red] "Oh! you missed to write commit message"
        return 0
    fi # closing statement of if-else block
    git push origin HEAD
}
```
```
function gitnew() {
    git checkout master
    git pull
    if [ "$1" != "" ]
    then
        git checkout -b "$1"
    else
        print $fg_bold[red] "Oh! you missed to write branch name"
        return 0
    fi # closing statement of if-else block
}

```
```
function npmnew() {
    if [ "$1" != "" ]
    then
        mkdir "$1"
    else
        print $fg_bold[red] "Project name to likh lo"
        return 0
    fi # closing statement of if-else block
    cd "$1"

    npm init -y
    touch server.js
    echo "node_modules/" > .gitignore
    git init
    git add .

    git commit -m "initial commit"
    git branch -M master
    
    if [ "$2" != "" ]
    then
        print $fg_bold[yellow] "Doing Remote Setup"
        gh repo create "$1" -y --public
    else
        print $fg_bold[yellow] "Local setup done"
        return 0
    fi # closing statement of if-else block
    git push -u origin master
    print $fg_bold[green] "SUCCESS-> Done Remote Setup"
}
```
