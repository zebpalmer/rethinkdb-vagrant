Vagrant::Config.run do |config|
  config.vm.define :master do |master_config|
    # Ubuntu 12.04, 64 bit
    master_config.vm.box     = "precise64"
    master_config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    # changing nictype partially helps with Vagrant issue #516, VirtualBox NAT interface chokes when
    # of slow outgoing connections is large (in dozens or more).
    # see https://github.com/mitchellh/vagrant/issues/912 regarding: --rtcuseutc
    master_config.vm.customize ["modifyvm", :id, "--memory", "512", "--ioapic", "on", "--rtcuseutc", "on"]

    master_config.ssh.username = "vagrant"
    master_config.vm.network :hostonly, "10.10.10.10"
    master_config.vm.forward_port 8080, 8080
    master_config.vm.forward_port 28015, 28015
    master_config.vm.forward_port 29015, 29015

    master_config.vm.provision :shell do |sh|
      sh.inline = <<-EOF
        export DEBIAN_FRONTEND=noninteractive;
        apt-get update --assume-yes;
        apt-get install --assume-yes python-software-properties;
        add-apt-repository --yes ppa:rethinkdb/ppa 2>&1;
        apt-get update --assume-yes;
        apt-get install --assume-yes rethinkdb;

        if [ ! -f /etc/rethinkdb/instances.d/default.conf ];
        then
          sed -e 's/somebody/root/g' -e 's/somegroup/root/g' /etc/rethinkdb/default.conf.sample > /etc/rethinkdb/instances.d/default.conf
          echo "bind=all" >> /etc/rethinkdb/instances.d/default.conf
          rethinkdb create -d /var/lib/rethinkdb/instances.d/default 2>&1;
        fi

        service rethinkdb start;
      EOF
    end
  end


  (1..11).each do |i|
    config.vm.define "slave#{i}" do |slave_config|
      # Ubuntu 12.04, 64 bit
      slave_config.vm.box     = "precise64"
      slave_config.vm.box_url = "http://files.vagrantup.com/precise64.box"

      # changing nictype partially helps with Vagrant issue #516, VirtualBox NAT interface chokes when
      # of slow outgoing connections is large (in dozens or more).
      # see https://github.com/mitchellh/vagrant/issues/912 regarding: --rtcuseutc
      slave_config.vm.customize ["modifyvm", :id, "--memory", "512", "--ioapic", "on", "--rtcuseutc", "on"]

      slave_config.ssh.username = "vagrant"
      slave_config.vm.network :hostonly, "10.10.10.1#{i}"
      slave_config.vm.forward_port 8080, 8081
      slave_config.vm.forward_port 28015, 28016
      slave_config.vm.forward_port 29015, 29016

      slave_config.vm.provision :shell do |sh|
        sh.inline = <<-EOF
          export DEBIAN_FRONTEND=noninteractive;
          apt-get update --assume-yes;
          apt-get install --assume-yes python-software-properties;
          add-apt-repository --yes ppa:rethinkdb/ppa 2>&1;
          apt-get update --assume-yes;
          apt-get install --assume-yes rethinkdb;

          if [ ! -f /etc/rethinkdb/instances.d/default.conf ];
          then
            sed -e 's/somebody/root/g' -e 's/somegroup/root/g' /etc/rethinkdb/default.conf.sample > /etc/rethinkdb/instances.d/default.conf
            echo "bind=all" >> /etc/rethinkdb/instances.d/default.conf
            echo "join=10.10.10.10:29015" >> /etc/rethinkdb/instances.d/default.conf
            rethinkdb create -d /var/lib/rethinkdb/instances.d/default 2>&1;
          fi

          service rethinkdb start;
        EOF
      end
    end
  end

end
