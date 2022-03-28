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
You can use this as
`$ gitpush your-commit-message`
and it will run following commands in order
```
git add .
git commit -m your-commit-message
git push origin head
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

You can use this as
`$ gitnew your-new-branch-name`
and it will run following commands in order
```
git checkout master
git pull origin master
git checkout -b your-new-branch-name
```
function npmnew() {
    if [ "$1" != "" ]
    then
        mkdir "$1"
    else
        print $fg_bold[red] "Oh! you missed to write project name"
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
