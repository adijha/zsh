## ALIAS
#aws

#golang
alias golang="nodemon --exec go run main.go --signal SIGTERM"

#docker
alias dock="docker-compose build && docker-compose up"
alias dockhide="docker-compose build && docker-compose up -d"

#git
alias githead="git push origin head"
alias gitmaster="git push origin master"
alias gitpull="git pull origin head"

#admin
alias admin='cd /Users/aditya.jha/admin-dashboard && concurrently "npm run serve" "npm run start"'
alias codeadmin='cd /Users/aditya.jha/admin-dashboard && code .  && concurrently "npm run serve" "npm run start"'
alias cdadmin='cd /Users/aditya.jha/admin-dashboard'

#dashboard
alias dash='cd /Users/aditya.jha/dashboard'
alias codedash='cd /Users/aditya.jha/dashboard && code .'
alias rundash='cd /Users/aditya.jha/dashboard && npm run serve'
alias mserve="cd /Users/aditya.jha/dashboard/public && ecstatic --cache 0 -H 'Access-Control-Allow-Origin: *'"

#devstack
alias devapi="cd /Users/aditya.jha/api && devspace dev --no-warn"
alias devterminals="cd /Users/aditya.jha/terminals && devspace dev --no-warn"
alias devfull='concurrently "cd /Users/aditya.jha/dashboard && devspace dev --no-warn" "cd /Users/aditya.jha/terminals && devspace dev --no-warn" "cd /Users/aditya.jha/api && devspace dev --no-warn"'
alias devbackend='concurrently "cd /Users/aditya.jha/terminals && devspace dev --no-warn" "cd /Users/aditya.jha/api && devspace dev --no-warn"'

#helmfile
alias helm='cd /Users/aditya.jha/kube-manifests/helmfile && helmfile delete && helmfile lint && helmfile sync'

## BASH FUNCTIONS

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
