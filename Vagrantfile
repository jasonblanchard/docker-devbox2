require 'yaml'

VAGRANTFILE_API_VERSION = "2"
DDB_CONFIG_PATH = File.expand_path(File.dirname(__FILE__)) + "/config.yml"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  ddb_config = YAML.load_file(DDB_CONFIG_PATH)

  ddb_config["services"].each do |docker_service, service_config|
    config.vm.define docker_service do |service|
      service.vm.provider "docker" do |d|
        d.name = docker_service
        service_config['docker_config'].each do |key, value|
          d.send("#{key}=", value)
        end
        d.vagrant_vagrantfile = "dproxy/Vagrantfile"
      end
    end
  end

end
