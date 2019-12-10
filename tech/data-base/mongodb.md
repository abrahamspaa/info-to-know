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
`mongorestore -d <local-database name> <path>` 

# Soruce:
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04


