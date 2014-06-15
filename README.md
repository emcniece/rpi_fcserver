rpi_fcserver
============

#### Raspberry Pi Fadecandy Server Init Scripts

This repository provides a quick-start guide for running the [Fadecandy](https://github.com/scanlime/fadecandy) server on a linux system. Clone this repo to your desired installation directory, then edit a couple files to match your setup.

While this was designed and tested on a Raspberry Pi, there is no reason it shouldn't work on other linux distros.

##### 1. Clone Repo

Download the files to your device. The first step here will change directory into your user, but you can install this anywhere else you desire. Just remember this server directory for later. Note that the git clone has the `--recursive` option - this is required for actually grabbing the fcserver package.


    $ cd ~
    $ git clone --recursive https://github.com/emcniece/rpi_fcserver.git


##### 2. Edit init files

We'll have to edit our service script to match our installation directory. If you're still in the current installation directory, you can find this path by taking the output of `pwd`.

###### $ nano ~/rpi_fcserver/rpi_fcserver

Change 2 lines to match your setup:


    INSTDIR=/root/rpi_fcserver/
    DAEMON_ARGS="$INSTDIR/rpi_fcconfig.json"


###### nano ~/rpi_fcserver/rpi_fcserver.json

Adjust fcserver config variables as needed. The default IP address of 127.0.0.1 may not work for you, so to quickly find your current IP address try reading the output of `/sbin/ifconfig eth0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}'`. If that doesn't work, try `ifconfig`.


##### 3. Install init files

Copy the init file to /etc/init.d and make it executable: 

    $ cp rpi_fcserver /etc/init.d/rpi_fcserver
    $ chmod 755 /etc/init.d/rpi_fcserver


##### 4. Build Fadecandy Server

As per the [build instructions](https://github.com/scanlime/fadecandy/tree/master/server):

    $ cd fadecandy/server
    $ make submodules
    $ make


##### 5. Test script and service

From the current directory of `fadecandy/server`, we can test our configuration by executing the following:

./fcserver ~/