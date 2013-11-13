# RethinkDB Cluster using Vagrant
Install [RethinkDB](http://rethinkdb.com) using [Vagrant](http://vagrantup.com).

## Quick Start -- One Liner
    git clone git@github.com:zebpalmer/rethinkdb-vagrant.git && \
        cd rethinkdb-vagrant && \
        ./rethinkdb.sh


## Cluster
To start the three node cluster run the quick start above, or if you've already cloned the repo
you can run "vagrant up". 

By default, you access the dashboard here:  
[http://localhost:8080/](http://localhost:8080/)

Three nodes are started 10.10.10.10, 10.10.10.11, 10.10.10.12 and can be accessed via localhost:8080-8082


To stop the Cluster, run "vagrant destory"



