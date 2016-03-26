# mean-setup

Designed to provide a simple way to setup a mean developer enviroment from scratch.

## NodeJs

```curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -```

```sudo apt-get update``` 

```sudo apt-get install nodejs``` 

*note that the '5' in the frist command is the current version if it gets outdated u just need to check the latest or stable version in http://nodejs.org.

check if the installation was successful by typing (or copy/paste):

```node -v```: what should geve you the current version of node instaled in you machine

and

```npm -v```: that is for the same porpouse above for node package manager

and thats it for NodeJS

##MongoDB

```sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10```

```sudo apt-get update```

```sudo apt-get install -y mongodb-org```

typing ```mongo -version``` should print out the current version of the mongo shell if everything went correctly.

Now in your system lets make the things easier:

###1- create de /data/db folder by typing:

  ```sudo mkdir /data && sudo mkdir /data/db```
  
  and change its permisson to the user: 
  ```sudo chown -R username:group /data```   (the username and group are your user name and group chang those to correspond)
  
  
In some cases mongod wont startup automacly with the system by default so use step 2

###2- set mongo server to start along the system:

  add mongod custom command to the startup applications
  
###3- set mongo-hacker:

  Mongo-Hacker is a nice feature for mongo shell and to install it just follow (https://github.com/TylerBrock/mongo-hacker).
  
  Download it:
  ```
 wget https://github.com/TylerBrock/mongo-hacker/archive/master.zip && unzip master.zip
  ```

  and then install it:
  ```
  cd mongo-hacker-master/ && sudo make && make install
  ```
  
  
###4- Disable warning messages:

  In most cases messages like bellow will show up everytime u start the shell:
  ```
  2015-03-06T21:01:15.526-0800 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/defrag is 'always'.
  2015-03-06T21:01:15.526-0800 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
  ```
  
  to prevent this follow the steps in this link:
  https://docs.mongodb.org/manual/tutorial/transparent-huge-pages/#transparent-huge-pages-thp-settings
  
  or just:
  
  create this script
  ```
  sudo touch /etc/init.d/disable-transparent-hugepages.sh && sudo gedit /etc/init.d/disable-transparent-hugepages.sh
  ```
  
  paste this content to it (u can use scratch or vi instead of gedit):
  ```
  #!/bin/sh
  ### BEGIN INIT INFO
  # Provides:          disable-transparent-hugepages
  # Required-Start:    $local_fs
  # Required-Stop:
  # X-Start-Before:    mongod mongodb-mms-automation-agent
  # Default-Start:     2 3 4 5
  # Default-Stop:      0 1 6
  # Short-Description: Disable Linux transparent huge pages
  # Description:       Disable Linux transparent huge pages, to improve
  #                    database performance.
  ### END INIT INFO
  
  case $1 in
    start)
      if [ -d /sys/kernel/mm/transparent_hugepage ]; then
        thp_path=/sys/kernel/mm/transparent_hugepage
      elif [ -d /sys/kernel/mm/redhat_transparent_hugepage ]; then
        thp_path=/sys/kernel/mm/redhat_transparent_hugepage
      else
        return 0
      fi
  
      echo 'never' > ${thp_path}/enabled
      echo 'never' > ${thp_path}/defrag
  
      unset thp_path
      ;;
  esac

  ```
  
  make it executable and set it in the startup:
  
  ```
  sudo chmod 755 /etc/init.d/disable-transparent-hugepages.sh && sudo update-rc.d disable-transparent-hugepages.sh defaults
  ```
  
  and then reboot your system to make the changes work.

