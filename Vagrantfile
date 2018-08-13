# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = "2"
  end

  config.vm.provider "hyperv" do |h|
    h.vm_integration_service = {
      guest_service_interface: true,
      heartbeat: true,
      key_value_pair_exchange: true,
      shutdown: true,
      time_syncronization: true,
      vss: true
    }
    h.cpus = "2"
    h.memory = "4096"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum makecache fast
    yum install -y git curl wget zip unzip
  SHELL
  config.vm.provision "shell", path: "https://raw.githubusercontent.com/oconnormi/packer-templates/master/centos/centos-7-jdk/scripts/install-sdkman.sh"
  config.vm.provision "shell", inline: <<-SHELL
    export SDKMAN_DIR="/usr/local/sdkman"
    source "/usr/local/sdkman/bin/sdkman-init.sh"
    sdk install java 8.0.181-oracle
    echo 'export PATH=/usr/local/sdkman/candidates/java/current/bin:$PATH' > /etc/profile.d/java.sh
    echo "export JAVA_HOME=/usr/local/sdkman/candidates/java/current" >> /etc/profile.d/java.sh
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    export SDKMAN_DIR="/usr/local/sdkman"
    source "/usr/local/sdkman/bin/sdkman-init.sh"
    sdk install maven
    echo 'export PATH=/usr/local/sdkman/candidates/maven/current/bin/:$PATH' > /etc/profile.d/maven.sh
    echo 'export M2_HOME=/usr/local/sdkman/candidates/maven/current/' >> /etc/profile.d/maven.sh
  SHELL
end
