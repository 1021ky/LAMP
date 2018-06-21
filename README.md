# LAMPython2

set up LAMP environment easyly
- L: Ubuntu16.04
- A: Apache2
- M: Mysql5.6
- P: Python2

## prerequisites

you need to install following software.

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](http://www.oracle.com/technetwork/jp/server-storage/virtualbox/downloads/index.html)
- vagrant plugin 'vbguest'

In addition to the above, you need to install vagrant plugin 'vagrant-proxyconf' on proxy network environment.
In addition to the above, you need to install rsync on Cygwin, MinGW or Bash On Ubuntu On Windows on windows.

## how to run

### at first 

run following commands.

* `vagrant box add ubuntu/xenial64`

You may skip those commands. But it takes much time to run `vagrant up` at first or after running `vagrant destory`.

### usual

run following commands.

* `vagrant up`

### shutdown

run following commands.

* `vagrant halt`


