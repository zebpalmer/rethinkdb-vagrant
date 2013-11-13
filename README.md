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


## Status
This is a third generation fork (love open source!) of a simple rethinkdb vagrant environment originally posted last year.
The original fork was a single instance, the intermediate fork added multiple nodes but was missing some config items
that were required (added in recent rethinkdb versions?). This version, should give you a working cluster with just the 
"vagrant up" command. This needs a bit more tlc to cleanup a bit and support more cluster nodes, perhaps even use the puppet
modules, but for now, it works. 



