# ubuntu

## How to install 
`sudo apt install -y mongodb`

## To See the status 
`systemctl status nginx`

## To see in the browser 
`http:localhost/`

## To stop 
`sudo systemctl stop mongodb`

## To start 
`sudo systemctl start mongodb`

## To restart 
`sudo systemctl reload mongodb`

## To Copy (mongo < 4.2)
`mongodump --uri="mongodb:<url>"`

## To restore to local
`mongorestore -d <local-database name> <path> or mongorestore <path>` 

# Mac

## Check monogo version 

`mongod --version`

## Checking monogo instant running 
`ps -ef | grep mongod | grep -v grep | wc -l | tr -d ' '`

## Start Monogo instant 
`brew services start mongodb-community@4.4`

## Stop Monogo instant

`brew services stop mongodb-community@4.4`

## brew service list 

`brew services list`

## Add path to access mongod

`vi ~/.zshrc`
`export PATH="$PATH:/usr/local/opt/mongodb-community@4.4/bin"`
`source ~/.zshrc`


# Soruce:
https://www.mongodb.com/docs/v4.4/tutorial/install-mongodb-on-os-x/
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/
To Remove https://stackoverflow.com/questions/48630553/homebrew-mongodb-connection-failed-mac-osx-sierra-10-12-6

