NUM_WORKER_NODES = 3
IMAGE_NAME = "ubuntu/focal64"
IP_NW = "192.168.50."
IP_START = 10

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.box_download_insecure = true

  config.vm.provision "shell", env: {"IP_NW" => IP_NW, "IP_START" => IP_START, "NUM_WORKER_NODES" => NUM_WORKER_NODES}, inline: <<-SHELL
    apt-get update -y
    echo "$IP_NW$((IP_START)) master-node" >> /etc/hosts
    for i in $(seq 1 $NUM_WORKER_NODES)
    do
      echo "$IP_NW$((IP_START+1)) worker-node$i" >> /etc/hosts
    done
  SHELL

  config.vm.box = IMAGE_NAME
  config.vm.box_check_update = true

  config.vm.define "master" do |master|
    master.vm.hostname = "master-node"
    master.vm.network "private_network", ip: IP_NW + "#{IP_START}"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = 4048
      vb.cpus = 2
    end
    master.vm.provision "shell", path: "scripts/common.sh"
    master.vm.provision "shell", path: "scripts/master.sh"
  end

  (1..NUM_WORKER_NODES).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "worker-node#{i}"
      node.vm.network "private_network", ip: IP_NW + "#{IP_START + i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
      end
      node.vm.provision "shell", path: "scripts/common.sh"
      node.vm.provision "shell", path: "scripts/node.sh"
    end
  end
end
