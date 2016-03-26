# mean-setup

Designed to provide a simple way to setup a mean developer enviroment from scratch.

## NodeJs

curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
sudo apt-get update
sudo apt-get install nodejs

*note that the '5' in the frist command is the current version if it gets outdated u just need to check the latest or stable version in http://nodejs.org.

check if the installation was successful by typing (or copy/paste):

node -v: what should geve you the current version of node instaled in you machine

and

npm -v: that is for the same porpouse above for node package manager

and thats it for NodeJS

##MongoDB

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

sudo apt-get update

sudo apt-get install -y mongodb-org

typing mongo -version should print out the current version of the mongo shell if everything went correctly.

Now in your system lets make the things easier:

###1- create de /data/db folder by typing:

  sudo mkdir /data && sudo mkdir /data/db
  
  and change its permisson to the user: sudo chown -R username:group /data   (the username and group are your user name and group chang those to correspond)
  
  
In some cases mongod wont startup automacly with the system by default so use step 2

###2- set mongo server to start along the system:

  add mongod custom command to the startup applications

