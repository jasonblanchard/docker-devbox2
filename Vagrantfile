# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'redis' do |redis|
    redis.vm.provider "docker" do |d|
      d.image =  "dockerfile/redis"
      d.ports = ["6379:6379"]
      d.vagrant_vagrantfile = "dproxy/Vagrantfile"
    end
  end

  config.vm.define 'mongo' do |mongo|
    mongo.vm.provider "docker" do |d|
      d.image = "ehazlett/mongodb"
      d.ports = ["27017:27017"]
      d.volumes = ["/home/vagrant/data:/tmp/mongo"]
      d.env = { "DATA_DIR" => "/tmp/mongo" }
      d.vagrant_vagrantfile = "dproxy/Vagrantfile"
    end
  end

  config.vm.define "app" do |app|
    app.vm.provider "docker" do |d|
      d.image = "jasonblanchard/ubuntu-rvm2"
      d.ports = ["3000:3000"]
      d.create_args = ['-i','-t']
      d.vagrant_vagrantfile = "dproxy/Vagrantfile"
      d.volumes = ["/home/vagrant/src:/src"]
    end
  end

end
