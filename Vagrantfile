require 'json'
require 'yaml'

VAGRANTFILE_API_VERSION = "2"
#confDir = $confDir ||= File.expand_path("~/.homestead")

#homesteadYamlPath = confDir + "/Homestead.yaml"
#afterScriptPath = confDir + "/after.sh"
#aliasesPath = confDir + "/aliases"

homesteadYamlPath = File.expand_path("./Homestead.yaml")
afterScriptPath = File.expand_path("./scripts/customize.sh")
aliasesPath = File.expand_path("./aliases")

require File.expand_path(File.dirname(__FILE__) + '/scripts/homestead.rb')

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "vmLaravelBox"
    config.vm.box_url = "http://fb-25dev/boxes/laravelBox.box"

    config.ssh.username = 'vagrant'
    config.ssh.password = 'vagrant'
    config.ssh.insert_key = 'true'

	if File.exists? aliasesPath then
		config.vm.provision "file", source: aliasesPath, destination: "~/.bash_aliases"
	end

	Homestead.configure(config, YAML::load(File.read(homesteadYamlPath)))

	if File.exists? afterScriptPath then
		config.vm.provision "shell", path: afterScriptPath
	end
end
